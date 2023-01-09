Bit Stuffing
#include<stdio.h>
#include<string.h>
int main()
{
int a[20],b[30],i,j,k,count,n;
printf("Enter frame size (Example: 8):");
scanf("%d",&n);
printf("Enter the frame in the form of 0 and 1 :");
for(i=0; i<n; i++)
scanf("%d",&a[i]);
i=0;
count=1;
j=0;
while(i<n)
{
if(a[i]==1)
{
b[j]=a[i];
for(k=i+1; a[k]==1 && k<n && count<5; k++)
{
j++;
b[j]=a[k];
count++;
if(count==5)
{
j++;
b[j]=0;
}
}
}
else
{
i=k;
}
i++;
j++;
}
b[j]=a[i];
printf("After Bit Stuffing :");
for(i=0; i<j; i++)
printf("%d",b[i])
return 0;
}
////////////////////////////////////////////////////////////////////////////////
Byte Stuffing
#include<stdio.h>
#include<string.h>
main()
{
char a[30], fs[50] = " ", t[3], sd, ed, x[3], s[3], d[3], y[3];
int i, j, p = 0, q = 0;
clrscr();
printf("Enter characters to be stuffed:");
scanf("%s", a);
printf("\nEnter a character that represents starting delimiter:");
scanf(" %c", &sd);
printf("\nEnter a character that represents ending delimiter:");
scanf(" %c", &ed);
x[0] = s[0] = s[1] = sd;
x[1] = s[2] = '\0';
y[0] = d[0] = d[1] = ed;
d[2] = y[1] = '\0';
strcat(fs, x);
for(i = 0; i < strlen(a); i++)
{
t[0] = a[i];
t[1] = '\0';
if(t[0] == sd)
strcat(fs, s);
else if(t[0] == ed)
strcat(fs, d);
else
strcat(fs, t);
}
strcat(fs, y);
printf("\n After stuffing:%s", fs);
getch();
}
///////////////////////////////////////////////////////////////////////////////////
CRC
#include<stdio.h>
#include<string.h>
#define N strlen(g)
char t[28],cs[28],g[]="10001000000100001";
int a,e,c;
void xor(){
 for(c = 1;c < N; c++)
 cs[c] = (( cs[c] == g[c])?'0':'1');
}
void crc(){
 for(e=0;e<N;e++)
 cs[e]=t[e];
 do{
 if(cs[0]=='1')
 xor();
 for(c=0;c<N-1;c++)
 cs[c]=cs[c+1];
 cs[c]=t[e++];
 }while(e<=a+N-1);
}
int main()
{
 printf("\nEnter data : ");
 scanf("%s",t);
 printf("\n----------------------------------------");
 printf("\nGeneratng polynomial : %s",g);
 a=strlen(t);
 for(e=a;e<a+N-1;e++)
 t[e]='0';
 printf("\n----------------------------------------");
 printf("\nModified data is : %s",t);
 printf("\n----------------------------------------");
 crc();
 printf("\nChecksum is : %s",cs);
 for(e=a;e<a+N-1;e++)
 t[e]=cs[e-a];
 printf("\n----------------------------------------");
 printf("\nFinal codeword is : %s",t);
 printf("\n----------------------------------------");
 printf("\nTest error detection 0(yes) 1(no)? : ");
 scanf("%d",&e);
 if(e==0)
 {
 do{
 printf("\nEnter the position where error is to be inserted : ");
 scanf("%d",&e);
 }while(e==0 || e>a+N-1);
 t[e-1]=(t[e-1]=='0')?'1':'0';
 printf("\n----------------------------------------");
 printf("\nErroneous data : %s\n",t);
 }
 crc();
 for(e=0;(e<N-1) && (cs[e]!='1');e++);
 if(e<N-1)
 printf("\nError detected\n\n");
 else
 printf("\nNo error detected\n\n");
 printf("\n----------------------------------------\n");
 return 0;
}
////////////////////////////////////////////////////////////////

DISTANCE
#include<stdio.h>
#include<string.h>
struct node
{
int dist[20];
int from[20];
}rt[10];
int main()
{
int dmat[20][20],i,j,k;
int n=i=j=k=0,count=0;
printf("Enter The Number of Nodes\n");
scanf("%d",&n);
printf("Enter The Cost Matrix\n");
for(i=0 ;i<n;i++)
for(j=0;j<n;j++)
{
scanf("%d",&dmat[i][j]);
dmat[i][i]=0;
rt[i].dist[j]=dmat[i][j];
rt[i].from[j]=j;
}
do
{
count=0;
for(i=0 ;i<n;i++)
for(j=0;j<n;j++)
for(k=0;k<n; k++)
if(rt[i] .dist[j]> dmat[i][k]+rt[k] .dist[j])
{
rt[i] .dist[j]=rt[i] .dist[k]+rt[k] .dist[j];
rt[i].from[j]=k;
count++;
}
}
while (count!=0);
for(i=0;i<n;i++)
{
printf("State Value For Router %d Is\n",i);
for(j=0;j<n;j++)
printf("\t\tVia %d Distance %d\n", rt[i].from[j],rt[i].dist[j]);
}
}
/////////////////////////////////////////////////////////////////////

DIJJ
#include<stdio.h>
#include<conio.h>
#define INFINITY 9999
#define MAX 10
void dijkstra(int G[MAX][MAX],int n,int startnode);
int main()
{
 int G[MAX][MAX],i,j,n,u;
 printf("Enter no. of vertices:");
 scanf("%d",&n);
 printf("\nEnter the adjacency matrix:\n");

 for(i=0;i<n;i++)
 for(j=0;j<n;j++)
 scanf("%d",&G[i][j]);

 printf("\nEnter the starting node:");
 scanf("%d",&u);
 dijkstra(G,n,u);

 return 0;
}
void dijkstra(int G[MAX][MAX],int n,int startnode)
{
 int cost[MAX][MAX],distance[MAX],pred[MAX];
 int visited[MAX],count,mindistance,nextnode,i,j;

 //pred[] stores the predecessor of each node
 //count gives the number of nodes seen so far
 //create the cost matrix
 for(i=0;i<n;i++)
 for(j=0;j<n;j++)
 if(G[i][j]==0)
 cost[i][j]=INFINITY;
 else
 cost[i][j]=G[i][j];

 //initialize pred[],distance[] and visited[]
 for(i=0;i<n;i++)
 {
 distance[i]=cost[startnode][i];
 pred[i]=startnode;
 visited[i]=0;
 }

 distance[startnode]=0;
 visited[startnode]=1;
 count=1;

 while(count<n-1)
 {
 mindistance=INFINITY;

 //nextnode gives the node at minimum distance
 for(i=0;i<n;i++)
 if(distance[i]<mindistance&&!visited[i])
 {
 mindistance=distance[i];
 nextnode=i;
 }

 //check if a better path exists through nextnode
 visited[nextnode]=1;
 for(i=0;i<n;i++)
 if(!visited[i])
 if(mindistance+cost[nextnode][i]<distance[i])
 {
 distance[i]=mindistance+cost[nextnode][i];
 pred[i]=nextnode;
 }
 count++;
 }
 //print the path and distance of each node
 for(i=0;i<n;i++)
 if(i!=startnode)
 {
 printf("\nDistance of node%d=%d",i,distance[i]);
 printf("\nPath=%d",i);

 j=i;
 do
 {
 j=pred[j];
 printf("<-%d",j);
 }while(j!=startnode);
 }
}
///////////////////////////////////////////////////////////////////////////////////


LEAK
#include<stdio.h>
#define BUCKET_MAX 10
#define FLOW_MAX 7
int main() {
int bucket=0, packets, outgoing;
for (int t = 1; ; t++) {
printf("\n\nAt Time t=%d sec\n", t);
printf("\nPackets in Bucket : %d\n", bucket);
printf("\nIncomming Packets : ");
scanf("%d", &packets);
if (packets+bucket>BUCKET_MAX) {
printf("\nPackets discarded : %d\n", packets+bucket-BUCKET_MAX);
bucket = BUCKET_MAX;
}
else {
printf("\nNo Packet Discarded\n");
bucket += packets;
}
if (bucket <= FLOW_MAX) {
outgoing = bucket;
}
else {
outgoing = FLOW_MAX;
printf("\nLimiting Flow\n");
}
printf("\nOutgoing Packets : %d\n", outgoing);
bucket -= outgoing;
}
return 0;
}
