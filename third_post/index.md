# Socket通信

# 前言
&emsp;&emsp;实现这个socket通信，我的方法是直接vim两个.c文件然后克隆一个终端，一个运行客户端，一个运行服务端，过程比较简单～
## 一、vim两个.c文件并且编译他们

![](/images/jietu11.png)

![](/images/jietu12.png)

其中client.c的代码：
```markdown
#include <stdio.h>
#include <stdlib.h>
#include <errno.h>		
#include <string.h>
#include <netdb.h>
#include <sys/types.h>
#include <netinet/in.h>
#include <sys/socket.h>
#include <arpa/inet.h>
#include <unistd.h>
int main(int argc,char *argv[]) 
{ 
int sockfd,numbytes; 
char buf[BUFSIZ]; 
struct sockaddr_in their_addr; 
printf("break!"); 
while((sockfd = socket(AF_INET,SOCK_STREAM,0)) == -1); 
printf("We get the sockfd~\n"); 
their_addr.sin_family = AF_INET; 
their_addr.sin_port = htons(8000); 
their_addr.sin_addr.s_addr=inet_addr("127.0.0.1"); 
bzero(&(their_addr.sin_zero), 8); 
while(connect(sockfd,(struct sockaddr*)&their_addr,sizeof(struct sockaddr)) == -1); 
printf("connect return: %d\n", connect(sockfd,(struct sockaddr*)&their_addr,sizeof(struct sockaddr))); 
printf("Get the Server~\n"); 
numbytes = recv(sockfd, buf, BUFSIZ,0);//接 收 服 务 器 端 信 息 
buf[numbytes]='\0'; 
printf("buf: %s\n",buf); 
while(1) 
{ 
printf("Entersome thing:"); 
scanf("%[^\n]%*c",buf); 
printf("scanf: %s\n", buf); 
numbytes = send(sockfd, buf, strlen(buf), 0); 
printf("send numbytes: %d\n", numbytes); 
numbytes=recv(sockfd,buf,BUFSIZ,0); 
printf("recv numbytes: %d\n", numbytes); 
buf[numbytes]='\0'; 
printf("received:%s\n",buf); 
} 
close(sockfd); 
return 0; 
} 
```
serve.c的代码：
```markdown
#include <stdio.h>
#include <stdlib.h>
#include <errno.h>		
#include <string.h>
#include <netdb.h>
#include <sys/types.h>
#include <netinet/in.h>
#include <sys/socket.h>
#include <arpa/inet.h>
#include <unistd.h>
int main(int argc, char *argv[]) 
{ 
int fd, new_fd, struct_len, numbytes,i; 
struct sockaddr_in server_addr; 
struct sockaddr_in client_addr; 
char buff[BUFSIZ]; 
server_addr.sin_family = AF_INET; 
server_addr.sin_port = htons(8000); 
server_addr.sin_addr.s_addr = INADDR_ANY; 
bzero(&(server_addr.sin_zero), 8); 
struct_len = sizeof(struct sockaddr_in); 
fd = socket(AF_INET, SOCK_STREAM, 0); 
while(bind(fd, (struct sockaddr *)&server_addr, struct_len) == -1); 
printf("Bind Success!\n"); 
while(listen(fd, 10) == -1); 
printf("Listening....\n"); 
printf("Ready for Accept,Waitting...\n"); 
new_fd = accept(fd, (struct sockaddr *)&client_addr, &struct_len); 
printf("accept return: %d\n", new_fd); 
printf("Get the Client~\n"); 
numbytes = send(new_fd,"Welcome to my server\n",21,0); 
while((numbytes = recv(new_fd, buff, BUFSIZ, 0)) > 0) 
{ 
buff[numbytes] = '\0'; 
printf("%s\n",buff); 
if(send(new_fd,buff,numbytes,0)<0) 
{ 
perror("write"); 
return 1; 
} 
} 
close(new_fd); 
close(fd); 
} 

```
## 二、运行测试是否能够运行成功

![](/images/jietu13.png)

![](/images/jietu14.png)

如上图所示，运行成功～

## 三、上传到github远程仓库
具体步骤请到我的首页查看“在ubantu中安装和配置git”这篇文章。

