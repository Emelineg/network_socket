#include <string.h>
#include <netdb.h>
#include <netinet/in.h>
#include <stdio.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>

int main(){
    int fd, err, errm, erecu; 
    struct sockaddr_in address;
    struct hostent *host;
    const char *msg;
    char buffer[1024];

    fd= socket(AF_INET, SOCK_STREAM, 0);

    host = gethostbyname("192.168.0.16");
    
    bzero(&address, sizeof(address));
    bcopy(host-> h_addr_list[0], &address.sin_addr, sizeof(address.sin_addr));
    address.sin_family = AF_INET;
    address.sin_port = htons(1234);

    err = connect(fd, (struct sockaddr*)&address, sizeof(address));

    if(err==0){
        printf("Connected\n");
        msg = "\n hello world";
        errm = send(fd, msg,strlen(msg) ,0);
        if(errm==-1)printf("erreur dans l'envoi\n");
        else printf("envoi OK\n");

        for(int i = 0; i<1024; i++) buffer[i] = '\0' ;

        erecu = recv(fd, buffer, sizeof(buffer)-1, 0);
        
        

        if(erecu== -1){
            printf(" receive fail\n");}
        else if(erecu==0){
            printf(" Connection closed\n");}
        else{
            printf(" Recu !!!\n");}

    }
    else{
        printf("not connected\n");}
    

    int c1 = close(fd);


    return 0;

}
