# x
just a repository
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX_ROOM_NUM        100
#define DATAFILENAME        "room.dat"//文件名（二进制）
struct Room
{
    char roomnumber[10];        //教室号
    char roomvalume[20];        //教室容量
    char roomplace[10];         //教室地点A,B,C,D
    char roomfloor[10];         //教室楼层
    char roomuse[8];            //教室状态
    char roomkind[10];          //类别
};

int roommax=0;

struct Room gRoom[MAX_ROOM_NUM];

int Menu1(int low,int up);

int Menu2(int low,int up);

void add();

void change();

void SearchByValume();

void search();

void SearchByNumber();

void SearchByPlace();

void show();

void WriteRoomInfo();

void ReadRoomInfo();
int main()
{
    int choice;
    system("color f4");
    ReadRoomInfo();
    do
    {
        choice=Menu1(1,6);
        switch(choice)
        {
            case 1:
                system("cls");
                add();
                break;
            case 2:
                system("cls");
                search();
                break;
            case 3:
                system("cls");
                show();
                break;
            case 4:
                system("cls");
                change();
                break;
            case 5:
                system("cls");
                del();
                break;
            default:
                system("cls");
                printf("\t\t\t\t---------------------------------------\n");
                printf("\t\t\t\t --- 谢谢使用教师信息管理系统5.0 ！--- \n");
                printf("\t\t\t\t---------------------------------------\n");
                break;
        }
    }
    while(choice!=6);
    return 0;
}
int Menu1(int low,int up)
{
    int choice;
    do
    {
        printf("\t\t\t\t----------------------------------------------\n");
        printf("\t\t\t\t---------------教室信息管理系统---------------\n");
        printf("\t\t\t\t---                                        ---\n");
        printf("\t\t\t\t---        欢迎使用教室信息管理系统5.0     ---\n");
        printf("\t\t\t\t---                                        ---\n");
        printf("\t\t\t\t----------------------------------------------\n");
        printf("\t\t\t\t---              1.录入教室信息            ---\n");
        printf("\t\t\t\t---              2.查找教室信息            ---\n");
        printf("\t\t\t\t---              3.显示教室信息            ---\n");
        printf("\t\t\t\t---              4.修改教室信息            ---\n");
        printf("\t\t\t\t---              5.删除教室信息            ---\n");
        printf("\t\t\t\t---              6.退出信息系统            ---\n");
        printf("\t\t\t\t----------------------------------------------\n");
        printf("\t\t\t\t---             请在1~6之间选择：          ---\n");
        printf("\t\t\t\t----------------------------------------------\n");
        scanf("%d",&choice);
        getchar();
    }
    while(choice<low || choice>up);
    return choice;
}
int Menu2(int low,int up)
{
    int choice;
    do
    {
        printf("\t\t\t\t-------------------------------\n");
        printf("\t\t\t\t---      1.按教室号查找     ---\n");
        printf("\t\t\t\t---      2.按容量查找       ---\n");
        printf("\t\t\t\t---      3.按地点查找       ---\n");
        printf("\t\t\t\t---      4.返回上一级菜单   ---\n");
        printf("\t\t\t\t-------------------------------\n");
        printf("\t\t\t\t--- 请在1~4之间选择查找方式 ---\n");
        printf("\t\t\t\t-------------------------------\n");
        scanf("%d",&choice);
        getchar();
    }
    while(choice<low || choice>up);
    return choice;
}
void add()
{
    int i;
    printf("请输入房间号：");
    gets(gRoom[roommax].roomnumber);
    for(i=0; i<roommax; i++)
    {
        if(strcmp(gRoom[roommax].roomnumber,gRoom[i].roomnumber)==0)
        {
            return ;
        }
    }
    printf("请输入教室容量：");
    gets(gRoom[roommax].roomvalume);
    printf("请输入地点：");
    gets(gRoom[roommax].roomplace);
    printf("请输入教室状态：");
    gets(gRoom[roommax].roomuse);
    printf("请输入教室种类：");
    gets(gRoom[roommax].roomkind);
    printf("请输入教室楼层:");
    gets(gRoom[roommax].roomfloor);
    roommax++;
    WriteRoomInfo();
    printf("添加成功！\n");
}
void change()
{
    char valume[20];
    char place[10];
    char use[8];
    char kind[10];
    char floor[10];
    int i;
    char roomnumber[10],ch;
    printf("请输入要修改的房间号:");
    gets(roomnumber);/*得到字符数组*/
    for(i=0; i<roommax; i++)
    {
        if(strcmp(gRoom[i].roomnumber,roomnumber)==0)
            break;
    }
    printf("你确定要修改该记录吗？(Y/N)\n");
    ch=getch();
    getchar();/*控制回车键，以免直接执行到下一步*/
    if(ch=='Y' || ch=='y')
    {
        getchar();
        printf("请重新输入教室容量：");
        gets(valume);
        strcpy(gRoom[i].roomvalume,valume);
        printf("请重新输入地点：");
        gets(place);
        strcpy(gRoom[i].roomplace,place);
        printf("请重新输入状态：");
        gets(use);
        strcpy(gRoom[i].roomuse,use);
        printf("请重新输入种类：");
        gets(kind);
        strcpy(gRoom[i].roomkind,kind);
        printf("请重新输入楼层：");
        gets(floor);
        strcpy(gRoom[i].roomfloor,floor);
        WriteRoomInfo();
        printf("\n成功修改1条记录！\n");
    }
}
void search()
{
    int choice;
    do
    {
        choice=Menu2(1,4);
        switch(choice)
        {
            case 1:
                SearchByNumber();
                break;
            case 2:
                SearchByValume();
                break;
            case 3:
                SearchByPlace();
                break;
            default:
                break;
        }
    }
    while(choice!=4);
}
void SearchByNumber()
{
    int i;
    char roomnumber[20];
    printf("请输入要查找的教室号:");
    gets(roomnumber);
    for(i=0; i<roommax; i++)
    {
        if(strcmp(gRoom[i].roomnumber,roomnumber)==0)
        {
            printf("%-10s%-10s%-10s%-10s%-10s%-10s\n",
                   "房间号","容量","地点","状态","种类","楼层");
            printf("%-10s%-10s%-10s%-10s%-10s%-10s\n",
                   gRoom[i].roomnumber,
                   gRoom[i].roomvalume,
                   gRoom[i].roomplace,
                   gRoom[i].roomuse,
                   gRoom[i].roomkind,
                   gRoom[i].roomfloor);
        }
    }
}
void SearchByValume()
{
    int i;
    char valume[20];
    printf("请输入要查找房间的容量:");
    gets(valume);
    for(i=0; i<roommax; i++)
    {
        if(strcmp(gRoom[i].roomvalume,valume)==0)
        {
            printf("%-10s%-10s%-10s%-10s%-10s%-10s\n",
                   "房间号","容量","地点","状态","种类","楼层");
            printf("%-10s%-10s%-10s%-10s%-10s%-10s\n",
                   gRoom[i].roomnumber,
                   gRoom[i].roomvalume,
                   gRoom[i].roomplace,
                   gRoom[i].roomuse,
                   gRoom[i].roomkind,
                   gRoom[i].roomfloor);
        }
    }
}
void SearchByPlace()
{
    int i;
    char place[20];
    printf("请输入要查找教室地点:");
    gets(place);
    for(i=0; i<roommax; i++)
    {
        if(strcmp(gRoom[i].roomplace,place)==0)
        {
            printf("%-10s%-10s%-10s%-10s%-10s%-10s\n",
                   "房间号","容量","地点","状态","种类","楼层");
            printf("%-10s%-10s%-10s%-10s%-10s%-10s\n",
                   gRoom[i].roomnumber,
                   gRoom[i].roomvalume,
                   gRoom[i].roomplace,
                   gRoom[i].roomuse,
                   gRoom[i].roomkind,
                   gRoom[i].roomfloor);
        }
    }
}
void show()
{
    int i;
    printf("%-10s%-10s%-10s%-10s%-10s%-10s\n",
           "房间号","容量","地点","状态","种类","楼层");
    for(i=0; i<roommax; i++)
    {

            printf("%-10s%-10s%-10s%-10s%-10s%-10s\n",
                   gRoom[i].roomnumber,
                   gRoom[i].roomvalume,
                   gRoom[i].roomplace,
                   gRoom[i].roomuse,
                   gRoom[i].roomkind,
                   gRoom[i].roomfloor);
    }
}

void WriteRoomInfo()
{
    int i;
    FILE *fp;
    /*打开文件*/
    if((fp=fopen(DATAFILENAME,"wb"))==NULL)
    {
        printf("打开文件%s失败！\n",DATAFILENAME);
        exit(1);
    }
    for(i=0; i<roommax; i++)
    {
        /*向二进制文件中写入数据*/
        fwrite((void *)&gRoom[i],sizeof(struct Room),1,fp);
    }
    /*关闭文件*/
    fclose(fp);
}
void ReadRoomInfo()
{
    FILE *fp;
    roommax=0;
    /*打开文件*/
    if((fp=fopen(DATAFILENAME,"rb"))==NULL)
    {
        return;
    }
    /*从二进制文件中读取数据*/
    while(feof(fp)==0)
    {
        if(fread((void *)&gRoom[roommax],sizeof(struct Room),1,fp)>0)
        {
            roommax++;
        }
    }
    /*关闭文件*/
    fclose(fp);
}








void del()
{
	char number[10];
	int i,k;
	char a;
	printf("请输入要删除的教室号: ");
	scanf("%s",number);
	printf("\n");
 	for(i=0;i<roommax;i++)
	{
		if(strcmp(gRoom[i].roomnumber,number)==0)
        {
			printf("要删除的教室号为:%s\n",number);
			printf("\n");
            printf("你确定要删除吗?继续请按'y',放弃请按'n'\n");
			printf("\n");
			printf("请选择:");
			scanf("%s",&a);
			if (a=='y'||a=='Y')
			{
			for(k=i;k<roommax;k++)
				{strcpy(gRoom[k].roomnumber, gRoom[k+1].roomnumber);
				strcpy(gRoom[k].roomvalume, gRoom[k+1].roomvalume);
				strcpy(gRoom[k].roomplace, gRoom[k+1].roomplace);
				strcpy(gRoom[k].roomuse, gRoom[k+1].roomuse);
				strcpy(gRoom[k].roomkind, gRoom[k+1].roomkind);
				strcpy(gRoom[k].roomfloor,gRoom[k+1].roomkind);
			    break;}
			}
			if(a=='n'||a=='N')
			{
printf("放弃删除!");
                return;
			}

				return;
		}
	}
	if(i==roommax)
		printf("!!!警告：姓名为%s的教室不存在!!!\n\n",number);
	else
	{
			printf("该教室已成功删除!重启后生效\n");
			roommax--;
	}
  	return ;
}

