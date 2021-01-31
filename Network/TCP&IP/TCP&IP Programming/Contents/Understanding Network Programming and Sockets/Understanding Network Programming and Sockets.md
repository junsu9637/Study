# 차례

[1. 네트워크 프로그래밍과 소켓의 이해](#understanding-network-programming-and-sockets)         
[1.1 네트워크 프로그래밍과 소켓의 이해](#understanding-network-programming-and-socket)             
[1.2 리눅스 기반 파일 조작](#linux-based-file-manipulation)           
[1.3 윈도우 기반 구현](#windows-based-implementation)              
[1.4 윈도우 기반의 소켓관련 함수](#windows-based-socket-related-functions)   

# Understanding Network Programming and Sockets   

## Understanding Network Programming and Socket    

**네트워크 프로그래밍**    
네트워크로 연결되어 있는 거로 다른 두 컴퓨터가 데이터를 주고받을 수 있도록 하는 것

소켓
물리적으로 연결된 네트워크 상에서의 데이터 송수신에 사용할 수 있는 소프트웨어적인 장치      
네트워크 망의 연결에 사용되는 도구

```C
// 소켓 생성
#include <sys/socket.h>
int socket(int domain, int type, int protocol);
```

```C
//IP주소와 PORT번호 할당
#include <sys/socket.h>
int bind(int sockfd, struct sockaddr *myaddr, socklen_t addrlen);
```

```C
// 연결요청 가능한 상태로 변경
#include <sys/socket.h>
int listen(int sockfd, int backlog);
```

```C
//연결요청에 대한 수락
#include <sys/socket.h>
int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
```

연결요청을 수락하는 기능의 프로그램을 서버(server)라고 한다. 연결요청 수락 시 "Hello world"라고 응답해주는 서버 프로그램을 작성하면 아래와 같다.
```C
// hello_server.c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>
#include <sys/socket.h>
void error_handling(char *message);

int main(int argc, char *argv[])
{
    int serv_sock;
    int clnt_sock;
    
    struct sockaddr_in serv_addr;
    struct sockaddr_int clnt_addr;
    socklen_t clnt_addr_size;
    
    char message[] = "Hello world";
    
    if (argc != 2)
    {
        printf("Usage : %s <port>\n", argv[0]);
        exit(1);
    }
    
    // socket 함수호출을 통해 소켓 생성
    serv_sock = socket(PF_INET, SOCK_STREAM, 0);
    if(serv_sock == -1)
    {
        error_handling("socket() error");
    }
    
    memset(&serv_addr, 0, sizeof(serv_addr));
    serv_addr.sin_family - AF_INET;
    serv_addr.sin_addr.s_addr = htonl(INADDR_ANY);
    serv_addr.sin_port = htons(atoi(argv[1]));
    
    // bind 함수호출을 통해 IP주소와 PORT번호 할당
    if(bind(serv_sock, (struct sockaddr*) &serv_addr, sizeof(serv_addr)) == -1)
    {
        error_handling("bind() error");
    }
    
    // listen 함수호출을 통해 소켓이 연결요청을 받아들일 수 있게 전환
    if(listen(serv_sock, 5) == -1)
    {
        error_handling("listen() error");
    }
    
    clnt_addr_size = sizeof(clnt_addr);
    // 연결요청 수락을 위한 accept 함수를 호출
    // 연결요청이 없는 상태에서 이 함수가 호출되면 연결요청이 있을 때까지 함수는 반환하지 않는다.
    clnt_sock = accept(serv_sock, (struct sockaddr*)&clnt_addr, &clnt_addr_size);
    if(clnt_sock == -1)
    {
        error_handling("accept() error");
    }
    
    // 데이터를 전송하는 함수
    write(clnt_sock, message, sizeof(message));
    close(clnt_sock);
    close(serv_sock);
    return 0;
}

void error_handling(char *message)
{
    fputs(message, stderr);
    fputs('\n', stderr);
    exit(1);
}
```
위에 예제를 통해 서버 소켓을 생성해 보았으니 이번에는 클라이언트 소켓을 생성해 보겠다.
```C
// 서버로의 연결요청
#include <sys/socket.h>
int connect(int sockfd, struct sockaddr *serv_addr, socklen_t addrlen);
```

```C
// hello_client.c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>
#include <sys/socket.h>
void error_handling(char *message);

int main(int argc, char* argv[])
{
    int sock;
    struct sockaddr_in serv_addr;
    char message[30];
    int str_len;
    
    if(argc != 3)
    {
        printf("Usage : %s <IP> <port>\n", argv[0]);
        exit(1);
    }
    
    // 소켓 생성
    // 소켓을 생성하는 순간에는 서버 소켓과 클라이언트 소켓으로 나뉘지 않는다.
    // bind, listen 함수의 호출이 이어지면 서버 소켓이 되는 것이고, connect 함수가 호출로 이어지면 클라이언트 소켓이 되는 것이다.
    sock = socket(PF_INET, SOCK_STREAM, 0);
    if(sock == -1)
    {
        error_handling("socket() error");
    }
    
    memset(&serv_addr, 0, sizeof(serv_addr));
    serv_addr.sin_family = AF_INET;
    serv_addr.sin_addr.s_addr = inet_addr(argv[1]);
    serv_addr.sin_port = htons(atoi(argv[2]));
    
    // connect 함수호출을 통해 서버 프로그램에 연결을 요청
    if(connect(sock, (struct sockaddr*)&serv_addr, sizeof(serv_addr)) == -1)
    {
        error_handling("connect() error");
    }
    
    str_len = read(sock, message, sizeof(message)-1);
    if(str_len == -1)
    {
        error_handling("read() error")
    }
    
    printf("Message from server : %s \n", message);
    close(sock);
    return 0;
}

void error_handling(char *mesage)
{
    fputs(message, stderr);
    fputs('\n', stderr);
    exit(1);
}
```

위 예제들을 리눅스 기반에서 컴파일 및 실행을 하기 위해서는 아래와 같은 단계를 거쳐야 한다.

```
gcc hello_server.c -o hserver
// hello_server.c 파일을 컴파일해서 hserver라는 이름의 실행파일을 만들어라 

./hserver
// hserver을 실행시켜라
```

## Linux-based file manipulation           

## Windows-based implementation              

## Windows-based socket-related functions  
