## For MacOS

https://trac.ffmpeg.org/wiki/CompilationGuide/macOS

## For Linux

```bash
sudo apt-get install bzip2 yasm nasm \
                build-essential automake autoconf \
                libtool pkg-config libcurl4-openssl-dev \
                intltool libxml2-dev libgtk2.0-dev \
                libnotify-dev libglib2.0-dev libevent-dev \
                checkinstall

wget https://www.ffmpeg.org/releases/ffmpeg-snapshot.tar.bz2

tar -xvf ffmpeg-snapshot.tar.bz2

cd ffmpeg
                
./configure --prefix=/usr/local/ffmpeg --enable-shared
sudo make
make install

export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/ffmpeg/lib/pkgconfig/
# add in at ~/.bashrc
# add in at ~/.zshrc

# check it by running
pkg-config --libs libavformat

sudo vim /etc/ld.so.conf
# add /usr/local/ffmpeg/lib/

sudo ldconfig

# deps of https://github.com/h2non/bimg
sudo apt install libvips-dev


gcloud auth application-default login

# migration and seeder setting located at scripts/development/run.sh
# .env file located at embeds/params/local/postgres.toml 

# migration
go run main.go migrate -t up -d="postgres"  --env=local  | sed G 

# seeder
go run main.go seed -t up -d="postgres"  --env=local  | sed G 

# run Go
go run main.go --env=local  | sed G 

# stop the app
sudo netstat -lpn |grep :3000

tcp6       0      0 :::3000                 :::*                    LISTEN      173571/main 

kill -9 <PID>

# deploy in server
gvm use go1.20.5 --default; cd ~/code/kai-ta-mobile-backend; git fetch origin; git pull origin; git describe --tags; GITHUB_TOKEN=ghp_xxxxxxx make release-with-publish; mv -f ~/code/kai-ta-mobile-backend/dist/*.tar.gz ~/; cd ~/; echo "extract compressed release :: "; find `pwd` -type f -name "*.tar.gz" -maxdepth 1 -exec tar -zxvf {} \;; echo "remove compressed release :: "; find `pwd` -type f -name "*.tar.gz" -maxdepth 1 -exec rm {} \;; echo "stop running process :: "; find `pwd`/apps -type f -name *stop.sh  -exec {} \;; sleep 10; echo "start running process :: "; find `pwd`/apps -type f -name *run.sh  -exec {} \;; sleep 10; echo "list running process :: "; pgrep -f "kai-ta-mobile-backend" -a
```
# TA-BE

## For Windows via Docker

1. configure the env files. embeds/params/local/machinery.toml
                                                postgres.toml
                                                chace.toml

```bash
docker compose up --build #run and build container
