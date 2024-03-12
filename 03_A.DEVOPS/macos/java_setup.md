/usr/libexec/java_home


gocode
https://gist.githubusercontent.com/tkawachi/2577734/raw/bd64e63507ce8ce4f1f2c158785e4df6395eb267/gistfile1.sh

PATH="$PATH:/usr/local/go/bin"
export GOBIN="$HOME/bin"
export PATH=$PATH:$HOME/bin
export GOPATH=/tmp
go get -u github.com/nsf/gocode
cd $GOPATH/src/github.com/nsf/gocode/vim/
./update.bash