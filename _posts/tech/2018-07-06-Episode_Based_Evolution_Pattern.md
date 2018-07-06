---
layout: blog
tools: true
istop: false
title: "Episode_Based_Evolution_Pattern "
background-image: https://3c1703fe8d.site.internapcdn.net/newman/csz/news/800/2017/howtowinthec.jpg
date:  2018-07-06 14:13:56
category: tools
tags:
- tools
- tech
- haze
---

# Episode Based Evolution Pattern

[Episode-Based Evolution Pattern Analysis of Haze Pollution: Method Development and Results from Beijing, China
Guangjie Zheng](https://pubs.acs.org/doi/abs/10.1021/acs.est.5b05593)

![pic1](https://pubs.acs.org/appl/literatum/publisher/achs/journals/content/esthag/2016/esthag.2016.50.issue-9/acs.est.5b05593/20160427/images/medium/es-2015-05593b_0009.gif)

## 附代码

Codes of the Module DevideEpi (Figure 1) in MATLAB M file format

```matlab

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%Input array & Parameters Needed: PMf, PMf24h, Missing Value; PMf24h_Thr; PMf_Thr%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%Input PMf; PMf= [number_of_timpoints,1]; time series of PM2.5 
%Input PMf24h; PMf24h = [number_of_timpoints,1]; time series of 24h-averaged PM2.5 conc. 
%centered at timepoint T. 
PMf24h_Thr = 75;    %_Thr value for level judge of PMf24h; 
PMf_Thr = 35;       %_Thr value for level judge of PMf;
MisVal=0;           %Value representing Missing Value

NumPnts=length(PMf); 
PMfLevel(1:NumPnts,1)=0; 
PMfLevel(find(PMf>PMf_Thr))=1; 
% PMfLevel= [timpoint,1]; if PMf>35, PMfLevel= 1,else, PMfLevel= 0 
PMf24hLevel(1:NumPnts,1)=0; 
PMf24hLevel(find(PMf24h>PMf24h_Thr))=1; 
% PMf24hLevel= [timpoint,1]; if PMf24h>75, PMf24hLevel= 1,else, PMf24hLevel= 0 
EpiChange(1:NumPnts,1)=0; 
EpiChange(2:NumPnts,1)=PMf24hLevel(2:NumPnts)-PMf24hLevel(1:NumPnts-1); 
EpiChgInd=find(EpiChange);     %or where epichange=1 and -1
EpiSup(1:NumPnts,1)=0;         %Remember where the epitag is changed by this program; 
EpiHourFlag(1:NumPnts,1)=0;    %Remember the type of PMf where 
                               %the epitag is changed by this program;
EpiNum=length(EpiChgInd);

for n=1:EpiNum 
       m = EpiChgInd(n);
       EpiChgType = EpiChange(m);
       if PMf(m)==MisVal                 %Episode Changed AT a data-missing period     
                   flag=-1; 
       elseif PMfLevel(m)==1             %Episode Changed at a polluted hour, search 
outside the episode
                AimType=0;               %look for the first clean hour
                ChangeValue=1;           %and all included hour should have EpiSup=1
                SearchType=EpiChgType;   %if Epi Start, type=1, look
backwards (back to previous timepoint); if Epi End, type=-1, look forward 
                flag=0;
       else                              %Episode Changed at a clean hour, search inside
the episode 
                AimType=1;               %look for the first polluted hour S11
                ChangeValue=-1;          %and all included hour should have EpiSup= -1
(excluded from the episode) 
                SearchType=-EpiChgType;     %if Epi Start, type=-1, look forward;        
                           %if Epi End, type=1, look backwards (back to previous timepoint)
                flag=0;
       end
       count=0; 

       while flag==0
             if SearchType==1 
                     m=m-1;            %look forwards for the first clean hour
             else
                     m=m+1;
             end           
             
             if PMf(m)==MisVal         %Episode Changed near a data-missing period         
                    flag=-1;
             elseif EpiChange(m)~=0    %meeting another episode
                    flag=2;            %False Episode Interval
             elseif PMfLevel(m)==AimType   %the first clean/polluted hour
                    flag=1;
             else
                    flag=0;
             end
             count=count+1;
        end
        
        if count>0
              if SearchType==1
                      EpiHourFlag((m+1):EpiChgInd(n)-1)= flag;
                      if flag>0
                             EpiSup((m+1):EpiChgInd(n)-1)= ChangeValue;
                      else
                             disp('Need Manual Decision on Missing Values')
                      end
              else
                      EpiHourFlag(EpiChgInd(n):(m-1))= flag;
                      if flag>0
                              EpiSup(EpiChgInd(n):(m-1))= ChangeValue;
                      else
                              disp('Need Manual Decision on Missing Values')
                      end
              end
        else
              EpiHourFlag(EpiChgInd(n)) = flag;
        end
end 
clear m n NumPnts SearchType EpiChgType EpiChgInd flag
clear AimType ChangeValue count EpiNum EpiChang
```

