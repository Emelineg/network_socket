#include <string.h>
#include <netdb.h>
#include <netinet/in.h>
#include <stdio.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/select.h>


int main(){
    int fd, err, s, n, errm, c;
    struct sockaddr_in address, remote;
    socklen_t remotelen;
    char buffer[1024];
    fd_set mySet, okSet;
    int maxfd = -1;


    fd= socket(AF_INET, SOCK_STREAM,0);

    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(1234);

    err = bind(fd,( struct sockaddr *)&address, sizeof(address));
    err = listen(fd,5);

    FD_ZERO(&mySet);
    FD_SET(fd,&mySet);
    if(fd>maxfd) maxfd=fd;

    while(1){
    //    FD_ZERO(&mySet);
    //    FD_SET(fd,&mySet);
        FD_COPY(&mySet,&okSet);
        n = select(maxfd+1, &okSet, NULL, NULL, NULL);

        for (int i=0; i<maxfd+1; i++){
            if(FD_ISSET(i,&okSet)){
                if(i==fd){
                    c= accept(fd, (struct sockaddr*)&remote, &remotelen);
                    FD_SET(c, &mySet);
                    if(s>maxfd)maxfd=c;
                }
                else{
                    
                    n = recv(i, buffer, sizeof(buffer)-1,0);
                                                
                    if(n == -1){
                        printf("\nreceive fail\n");}
                //    else if(n==0){
                //        printf("fermeture de la socket\n");
                //    }
                    else if(n>0){
                        printf("Recu !!!\n");
                        errm = send(i, buffer, sizeof(buffer)-1, 0);
                        if(errm==-1){
                            printf("didn't work\n");
                        }        
                        else if(errm > 0){
                            printf("renvoye\n");}
                        int c2 = close(i);

                        }
                }
            }
        }
    }

    
    int c1 = close(fd);

    return 0;
}
