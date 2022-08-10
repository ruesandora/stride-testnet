# 155420. blok ulaşanlar güncelleme yapsın !

```
sudo systemctl stop strided
cd $HOME
rm -rf stride
git clone https://github.com/Stride-Labs/stride.git && cd stride
git checkout 4ec1b0ca818561cef04f8e6df84069b14399590e 
make build
sudo cp $HOME/stride/build/strided /usr/local/bin
sudo systemctl restart strided && journalctl -fu strided -o cat
```
