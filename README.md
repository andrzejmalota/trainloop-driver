## Training

### Logging in to the EC2 machine

```
ssh -i training-identity.pem ec2-user@<EC2 VM>
mosh ec2-user@<EC2 VM>
```

### Setting up the EC2 machine

```
sudo yum update 
sudo yum install htop tmux docker python3 python3-pip mosh-server
```

### Installing mosh-server on EC2

```
sudo yum -y install autoconf automake gcc gcc-c++ make boost-devel zlib-devel ncurses-devel protobuf-devel openssl-devel
wget http://mosh.mit.edu/mosh-1.3.2.tar.gz
tar zxvf mosh*
cd mosh*
./configure
make
sudo make install
cd ..
rm -rf mosh*
```

### Accessing dumps of data from SAMM and dnnevo

```
version: '3'
services:
  dnnevodb:
    image: postgres:10
    environment:
      - POSTGRES_USER=samm
      - POSTGRES_PASSWORD=samm
      - POSTGRES_DB=samm
      - PGDATA=/storage
    volumes:
      - ./ignored/pgdata:/storage
    ports:
      - "5432:5432"

  sammdb:
    image: postgres:11
    environment:
      - POSTGRES_USER=samm
      - POSTGRES_PASSWORD=samm
      - POSTGRES_DB=samm
      - PGDATA=/storage
    volumes:
      - ./ignored/sammdata:/storage
    ports:
      - "5432:5432"
```
