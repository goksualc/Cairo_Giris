
# Cairo Diline Giriş

![My Image](cairo_logo.png)


## Environment Kurulumu

Kurulumlarda yer alan komutları Linux veya Mac terminalinize yazmanız gerekiyor. Windows kullanıcıları  [*Ubuntu for Windows*](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-10#3-download-ubuntu)'u indirerek komutları Ubuntu terminaline yazabilir. 


### Kurulum
- Python sanal ortamı içinde çalışmanızı öneriliyor, ancak doğrudan Cairo paketini de kurabilirsiniz. Sanal ortamı oluşturmak ve girmek için terminalinize şu komutu yazmalısınız:

````bash
python3.9 -m venv ~/cairo_venv
source ~/cairo_venv/bin/activate
````

Bu komuttan sonra terminal ekranınızda ***cairo_venv *** yazısını görmeniz gerekiyor. 

- Daha sonrasında ***Ubuntu*** kullanıcılarının önce şunları çalıştırması gerekir:

````bash 
sudo apt install -y libgmp3-dev
````

- Mac kullancıları ise şu komutu girmeli:

````bash
brew install gmp
````

- Aşağıdakileri kullanarak ***Cairo-Lang***  Python paketini kurun:

````bash
pip3 install cairo-lang
````

> Alternatif olarak, paketi **(cairo-lang-0.10.3.zip)** https://github.com/starkware-libs/cairo-lang/releases/tag/v0.10.3 adresinden ya da aşağıdaki komutu kullanarak indirebilirsiniz.

````bash
pip3 install cairo-lang-0.10.3.zip
````
- Cairo, python3.9 ile test edildi. Python3.6 ile çalışmasını sağlamak için contextvars kurmanız gerekecek:

````bash
pip3 install contextvars
````






