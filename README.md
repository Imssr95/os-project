#include<stdio.h>
#include<time.h>
struct prior
{
char process_name[10];
int arr_time,Bur_time;
int exec;
float wait_time,turnar_time;
float priority;
}pr[20],pr1[20],tempoo;
int ta=0,tot_bt=0,n;
void calc_priority()			
{    int i;
for(i=0;i<n;i++)
{
 if(pr[i].exec==0)		
 {
if(pr[i].arr_time<=tot_bt)
{	
if(pr[i].Bur_time==0)
{
pr[i].wait_time=tot_bt-pr[i].arr_time;
pr[i].priority=9999;							
}
else
{
pr[i].wait_time=tot_bt-pr[i].arr_time;
pr[i].priority=1+(pr[i].wait_time/pr[i].Bur_time);
}
}
 }
}
}
void prior_sort()			
{	int i,j;
for(i=0;i<n-1;i++)
{
for(j=0;j<n-i-1;j++)
{		
if(pr[j].priority<pr[j+1].priority)	
{
tempoo=pr[j];
pr[j]=pr[j+1];				
pr[j+1]=tempoo;
}
}
}
pr[0].exec=1;			
pr1[ta]=pr[0];
for(i=0;i<n;i++)
{
pr[i].priority=0;
 }
}
void main()
{
int i,j;
printf("Define the number of processes");
scanf("%d",&n);								
for(i=0;i<n;i++)
{
printf("enter process %d name:",i+1);
scanf("%s",&pr[i].process_name);               
printf("Define the arrival time");
scanf("%d",&pr[i].arr_time);
printf("Define the burst time:");
scanf("%d",&pr[i].Bur_time);		
}
for(i=0;i<n;i++)
{
pr[i].exec=0;		
pr[i].priority=0;
}
    for(i=0;i<n-1;i++)
{
for(j=0;j<n-i-1;j++)
{
if(pr[j].arr_time>pr[j+1].arr_time)			
{
tempoo=pr[j];
pr[j]=pr[j+1];				
pr[j+1]=tempoo;
}
}
}   
pr[0].exec=1;   		
pr1[ta]=pr[0];
ta++;
tot_bt=pr[0].arr_time+pr[0].Bur_time;
for(i=0;i<n-1;i++)
{  
calc_priority();		
prior_sort();
tot_bt+=pr[0].Bur_time;		
ta++;	
}
int max_bt=pr1[0].arr_time+pr1[0].Bur_time;
pr1[0].wait_time=0;
pr1[0].turnar_time=pr[i].Bur_time;
for(i=1;i<n;i++)
{
pr1[i].wait_time=max_bt-pr1[i].arr_time;				
pr1[i].turnar_time=pr1[i].wait_time+pr1[i].Bur_time;	
max_bt+=pr1[i].Bur_time;
}
printf("Process	   arr_time     Bur_time    waiting time     turnar_time time");
for(i=0;i<n;i++)
{
printf(" %s  %d    %f    %f",pr1[i].process_name,pr1[i].arr_time,pr1[i].Bur_time,pr1[i].wait_time,pr1[i].turnar_time);
}
float Avg_turnar_time=0,Avg_waiting=0;
int t=0;
for(i=0;i<n;i++)
{   
if(pr1[i].Bur_time!=0)
{
t++;
Avg_turnar_time+=pr1[i].turnar_time;		
Avg_waiting+=pr1[i].wait_time;
}
}
Avg_turnar_time/=t;
Avg_waiting/=t;
printf("\n------------------------------------------------------------------------------\n");
printf("Average Turn Around Time=%f\n",Avg_turnar_time);
printf("Average Waiting time=%f\n",Avg_waiting);
}
