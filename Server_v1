#include <string.h>
#include <netdb.h>
#include <netinet/in.h>
#include <stdio.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>

int main(){
    int fd, err, s, recu, errm;
    struct sockaddr_in address, remote;
    socklen_t remotelen;
    char buffer[1024];


    fd= socket(AF_INET, SOCK_STREAM,0);

    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(1234);


    err=bind(fd,(struct sockaddr *)&address, sizeof(address));
    err= listen(fd,5);
    s = accept(fd,(struct sockaddr *)&remote, &remotelen);

    if (s == -1){
        printf("Erreur dans la reception");
    }
    else if (s > 0){
        for(int i=0; i<1024; i++) buffer[i] = '\0'; 
        recu = recv(s, buffer, sizeof(buffer)-1, 0);
        if(recu == -1){
            printf("\nreceive fail\n");}
        else if(recu>0){
            printf("\nRecu !!!\n");
            errm = send(s, buffer, sizeof(buffer)-1, 0);
            if(errm==-1){
                printf("didn't work\n");
            }
            else if(errm > 0){
                printf("renvoye\n");}
            int c2 = close(s);

            }
        }
    
    int c1 = close(fd);

    return 0;
}
