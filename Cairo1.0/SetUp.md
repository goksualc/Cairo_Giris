
# Kurulum

## Cairo 1.0 Compiler Kurulumu

- Cairo'yu ilk defa indiriyorsanız: 

````bash
git clone https://github.com/starkware-libs/cairo/
cd cairo
git checkout 9c190561ce1e8323665857f1a77082925c817b4c
cargo build --all --release
`````

- Eğer cairo bilgisayarınızda yüklü ise: 
````bash
cd cairo
git fetch && git pull
git checkout 9c190561ce1e8323665857f1a77082925c817b4c
cargo build --all --release
````

## Environment Kurulumu
- Kurulumlarda yer alan komutları Linux veya Mac terminalinize yazmanız gerekiyor. Windows kullanıcıları  [*Ubuntu for Windows*](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-10#3-download-ubuntu)'u indirerek komutları Ubuntu terminaline yazabilir. 


### Cairo-lang Kurulumu
- Python sanal ortamı içinde çalışmanızı öneriliyor, ancak doğrudan Cairo paketini de kurabilirsiniz. Sanal ortamı oluşturmak ve girmek için terminalinize şu komutu yazmalısınız:

````bash
python3.9 -m venv ~/cairo_venv_v11
source ~/cairo_venv_v11/bin/activate
````

Bu komuttan sonra terminal ekranınızda ***cairo_venv *** yazısını görmeniz gerekiyor. 

Daha önceden kurulum yaptıysanız uninstall edip tekrar kurulum yapmanız gerekiyor: 

````bash
pip3 uninstall cairo-lang
`````
En son versionunu kuruyoruz. 
````bash 
pip3 install cairo-lang-0.11.0.1.zip
````
> Alternatif olarak, paketi **(cairo-lang-0.11.0.1.zip)** [https://github.com/starkware-libs/cairo-lang/releases/tag/v0.10.3 ](https://github.com/starkware-libs/cairo-lang/releases/tag/v0.11.0.1) adresinden de indirebilirsiniz. 

Starkneti doğru indirip indirmediğinizi aşağıdan test edebilirsiniz: 

````bash
starknet --version 
````

Tebrikler kurulumu tamamladınız! 


