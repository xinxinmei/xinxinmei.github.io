# 开发环境
##  使用codeclock软件进行编程
* 新建项目选择console application完成相应的步骤即可。在项目下有main.c的文件只需要将代码写入其中即可。
## 代码设计
* 客户端
client
```swift
#include <stdio.h>
#include <stdlib.h>
#include <winsock2.h>
#define  MAX_DATA_BLOCK_SIZE 8192
void error_exit(const char * msg,int val);
void send_file(const char * file_name,const char * ip,u_short port);
int main(int argc,char** argv){
    u_short port;
    if(argc==3){
        send_file(argv[1],argv[2],8888);
    }
    else if(argc==4){
        port=(u_short) atoi(argv[1]);
        if(port==0){
            error_exit("非法服务器端口",-1);
        }else{
            send_file(argv[1],argv[2],port);
        }
    }
    else{
        error_exit("参数错误",-1);
    }
    return 0;
}
void error_exit(const char* msg, int val){
    if(msg){
        printf("%s\n\n",msg);
        }
    printf("使用方式： ft_client<文件名><服务器IP地址>[服务器端口]\n");
    printf("服务器端口是可选参数，默认为8888\n\n");
    exit(val);
}
void send_file(const char* file_name,const char* ip, u_short port){

    WSADATA wsaData;
    SOCKET s;
    FILE *fp;
    struct sockaddr_in server_addr;
    char data[MAX_DATA_BLOCK_SIZE];
    int i;
    int ret;
    fp=fopen(file_name,"rb");
    if(fp==NULL){
        printf("无法打开文件\n");
        return;
        }
    WSAStartup(0x202,&wsaData);
    s=socket(AF_INET,SOCK_STREAM,0);
    memset((void *)&server_addr,0,sizeof(server_addr));
    server_addr.sin_family=AF_INET;
    server_addr.sin_addr.s_addr=inet_addr(ip);
    server_addr.sin_port=htons(port);
    if(connect(s,(struct sockaddr *)&server_addr,sizeof(struct sockaddr_in))==SOCKET_ERROR){
        printf("连接服务器失败\n");
        fclose(fp);
        closesocket(s);
        WSACleanup();
        return;
        }
    printf("发送文件名。。。\n");
    send(s,file_name,strlen(file_name),0);
    send(s,"\0",1,0);
    printf("发送文件内容");
    for(;;){
        memset((void *)data,0,sizeof(data));
        i=fread(data,1,sizeof(data),fp);
        if(i==0){
            printf("\n发送成功\n");
            break;
            }
        ret=send(s,data,i,0);
        putchar('.');
        if(ret==SOCKET_ERROR){
            printf("\n发送失败，文件可能不完整\n");
            break;
            }
        }
    fclose(fp);
    closesocket(s);
    WSACleanup();


}

```

* 服务器端
server
```swift
#include <stdio.h>
#include <stdlib.h>
#include <process.h>
#include <winsock2.h>
#define MAX_DATA_BLOCK_SIZE 8192
void error_exit(const char *msg, int val);
void serve_at(u_short port);
void serve_client(void *s);
void print_socket_detail(SOCKET s);

int main(int argc,char ** argv){
    u_short port;
    if(argc==1){
        serve_at(8888);
        }
    else if(argc==2){
        port=(u_short) atoi(argv[1]);
        if(port==0){
            error_exit("非法的监听端口",-1);
            }
        else{
            serve_at(port);
            }
        }
    else{
       error_exit("参数错误",-1);
        }
    return 0;
}

void error_exit(const char * msg, int val){
    if(msg){printf("%s\n\n",msg);}
    printf("使用方法：ft_server [监听端口]\n");
    printf("监听端口是可选参数，默认为8888\n\n");
    exit(val);

}
void serve_at(u_short port){
    WSADATA wsaData;
    SOCKET ls,as;
    static SOCKET *a;
    struct sockaddr_in addr;
    struct sockaddr_in cli_addr;
    int cli_addr_len;
    WSAStartup(0x202,&wsaData);
    ls=socket(AF_INET,SOCK_STREAM,0);
    memset((void *)&addr,0,sizeof(addr));
    addr.sin_family=AF_INET;
    addr.sin_addr.s_addr=inet_addr("0.0.0.0");
    addr.sin_port=htons(port);
    bind(ls, (struct sockaddr *)&addr,sizeof(addr));
    listen(ls, SOMAXCONN);
    printf("服务器已启动，监听于端口%d\n",port);
    for(;;){
        cli_addr_len=sizeof(cli_addr);
        memset((void *)&cli_addr,0,cli_addr_len );
        as=accept(ls,(struct sockaddr *)&cli_addr,&cli_addr_len);
        a=&as;
        printf("客户端%s:%d已连接\n",inet_ntoa(cli_addr.sin_addr),ntohs(cli_addr.sin_port));
        _beginthread(serve_client,0,(void *)a);
        Sleep(1000);
        print_socket_detail(as);
        // while(1){}
        }
    closesocket(ls);
    WSACleanup();
}


void serve_client(void *s){
         printf("\n\n\n创建新线程成功！\n\n\n");
        char file_name[MAX_PATH];
        char data[MAX_DATA_BLOCK_SIZE];
        int i;
        char c;
        FILE *fp;
        printf("接收文件名。。。。\n");
        memset((void *)file_name,0, sizeof(file_name));
        for(i=0; i<sizeof(file_name);i++){
            if(recv(*(SOCKET *)s,&c,1,0)!=1){
                printf("接收失败或客户端已关闭连接\n");
                closesocket(*(SOCKET *)s);
                return;
                }
            if(c==0){
                break;
                }
            file_name[i]=c;
            }
        if(i==sizeof(file_name)){
            printf("文件名过长\n");
            closesocket(*(SOCKET *)s);
            return;
            }
        printf("文件名%s\n",file_name);
        fp=fopen(file_name,"wb");
        if(fp==NULL){
            printf("无法以写方式打开文件\n");
            closesocket(*(SOCKET *)s);
            return;
        }
        printf("接收文件内容");
        memset((void *)data, 0,sizeof(data));
        for(;;){

            i=recv(*(SOCKET *)s,data,sizeof(data),0);
            putchar('.');
            if(i==SOCKET_ERROR){
                printf("\n接收失败，文件可能不完整\n");
                break;
                }
            else if(i==0){
                printf("\n接收成功\n");
                break;
                }
            else{
               // fwrite((void *)data,1,i,fp);
                }
            }
        printf("%s",data);
        fclose(fp);_endthread();
        closesocket(*(SOCKET *)s);

}


void print_socket_detail(SOCKET s){
    struct sockaddr_in name;
    int namelen;
    namelen=sizeof(name);
    memset(&name,0,namelen);
    getsockname(s,(struct sockaddr*)&name, &namelen);
    printf("local:%s:%d\n",inet_ntoa(name.sin_addr),ntohs(name.sin_port));
    namelen=sizeof(name);
    memset(&name,0,namelen);
    getpeername(s,(struct sockaddr*)&name,&namelen);
    printf("peer:%s:%d\n",inet_ntoa(name.sin_addr),ntohs(name.sin_port));
  }


```
## 相关知识点
1.如果建立的项目中没有连接Ws2_32.lib库的话需要在函数的开始添加``#pragma comment(lib, "Ws2_32.lib")``
2.本次编程中我加入了多线程以满足多个client的与server连接的需求。
使用了_beginthread()函数包含于process.h头文件中，有关于[_beginthread()函数方法](https://baike.baidu.com/item/beginthread/4230822)如果对于void *不了解的可以查阅相关资料。

### 注意
在多线程的使用当中应该注意多线程的特性，在server的代码中``  _beginthread(serve_client,0,(void *)a);
        Sleep(1000);``我使用了sleep（）等待了一秒，如果不使用可能会导致as变量在未执行到相关的处理函数的时候就被释放了（导致后面读取文件失败）因为as是局部变量，解决方法可以将它设为全局变量或者静态变量，但都不适合。所以我使用了sleep（）虽然也不是好的方法。

