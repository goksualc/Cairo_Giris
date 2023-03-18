
# Cairo Diline Giriş

*StarkNet*, Ethereum üzerinde bir L2 ağı olarak çalışan izinsiz (permissionless), merkezi olmayan bir ZK-Rollup'tır.

*Cairo*, bir tarafın diğerine belirli bir hesaplamanın doğru yürütüldüğünü kanıtlayabildiği kanıtlanabilir programlar yazmak için bir programlama dilidir. Cairo ve benzeri ispat sistemleri, blok zincirlerine ölçeklenebilirlik sağlamak için kullanılabilir.

> StarkNet, hem altyapısı hem de StarkNet sözleşmelerini yazmak için **Cairo** programlama dilini kullanır.

## Enviroment Kurulumu

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

## Cairo Programını Çalıştırma

- İsmi ***test.cairo*** olan bir dosya oluşturarak başlıyoruz. Dosyamızın içine aşağıda yer alan kodları yapıştırıyoruz. VS Code yardımı ile dosyayı düzenleyebilirsiniz. 

````bash
func main() {
[ap] = 1000, ap++;
    [ap] = 2000, ap++;
[ap] = [ap - 2] + [ap - 1], ap++;
ret;
}
````

-  Compile edin. Tüm komutların virtual environment'ta gerçekleştiğinden emin olmalısınız. ( ***cairo_venv*** yazısını görüyor olmalısınız)

````bash
cairo-compile test.cairo --output test_compiled.json
````

*Bu komutla test_compiled.json dosyasını oluşturmuş oluyorsunuz. *

- Programı çalıştırın. 
````bash
cairo-run \
--program=test_compiled.json --print_output \
--print_info --relocate_prints
````
*Bunun sonucu olarak şöyle bir **output** görmelisiniz:*

````bash
Number of steps: 4 (originally, 4)
Used memory cells: 11
Register values after execution:
pc = 12
ap = 12
fp = 12
````

- --tracer bayrağını cairo-run'a sağlayarak Cairo tracer'ını açabilirsiniz. 
````bash
cairo-run --program test_compiled.json --tracer
````
*Ardından http://localhost:8100/ adresini açmalısınız.*


İşte bu kadar ilk programınızı çalıştırdınız, ***Tebrikler!***




