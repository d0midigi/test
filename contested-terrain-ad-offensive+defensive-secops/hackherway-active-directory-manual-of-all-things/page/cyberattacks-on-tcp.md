# Cyberattacks on TCP

// Step 1: Create a socket.

int sockfd = socket (AF\_INET, SOCK\_STREAM, 0);

// Step 2: Set the destination information\
struct sockaddr\_in dest;

memset (\&dest, 0, sizeof(struct sockaddr\_in));

dest.sin\_family = AF\_INET;

dest.sin\_addr.s\_addr = inet\_addr (“10.0.2.17”);

dest.sin\_port = htons(9090);

// Step 3: Connect to the server

connect(sockfd, (struct sockaddr \*) \&dest,

sizeof(struct sockaddr\_in));

// Step 4: Send data to the server

char \*buffer1 = “Hello Server!\n”;

char \*buffer2 = “Hello Again!\n”;

write (sockfd, buffer1, strlen(buffer1));

write(sockfd, buffer2, strlen(buffer2));
