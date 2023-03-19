
# Cairo Programını Çalıştırma

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




