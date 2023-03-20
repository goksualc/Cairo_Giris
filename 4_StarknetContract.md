
### İlk Kontrat

- first_contract.cairo isimli kontratımızı Starknet'e deploy edeceğiz. Bunun için aşağıdaki komutu kullanmamız gerekiyor: 

````bash 
starknet-compile first_contract.cairo \
    --output first_contract_compiled.json \
    --abi first_contract_abi.json
	````

Bu komuttan sonra first_contract_abi.json isimli bir json dosyası oluşturmuş oluyoruz. ABI dosyası, çağrılabilir tüm fonksiyonların ve bunların beklenen inputlarının bir listesini içeriyor.

### Sözleşmeyi StarkNet Testnet Üzerinde Declare Etme

- CLI'ye StarkNet testnet ile çalışması talimatını vermek için ya her kullanımda --network=alpha-goerli'yi geçmeli ya da STARKNET_NETWORK ortam değişkenini aşağıdaki gibi ayarlamalısınız:
````bash
export STARKNET_NETWORK=alpha-goerli
````
- Kontrat sınıfınızı StarkNet test ağında declare etmek için aşağıdaki komutu çalıştırmalısınız:
````bash
starknet declare --contract first_contract_compiled.json
````

Örnek **output**:

````bash
Declare transaction was sent.
Contract class hash: 0x1e2208b571b2cb68908f37a196ed5e391c8933a6db23bb3939acedee40d9b8a
Transaction hash: 0x762e166dd3326b2e263eb5bcfdccd225dc88e067fdf7c92cf8ce5e4ea01f9f1
````
Yeni kontratınızın class hash'ini burada görebilirsiniz. Deploy sistem çağrısını kullanarak kontratın bir örneğini dağıtmak için bu class hash'ine ihtiyacınız olacak.

### Kontratı StarkNet Test Ağında Deploy Edin
- Kontratınızı StarkNet test ağında deploy etmek için aşağıdaki komutu çalıştırmalısınız ($CLASS_HASH'ı starknet declare'inden aldığınız class hash ile değiştirmelisiniz):
````bash
starknet deploy --class_hash $CLASS_HASH
````
Örnek output: 
````bash 
Invoke transaction for contract deployment was sent.
Contract address: 0x039564c4f6d9f45a963a6dc8cf32737f0d51a08e446304626173fd838bd70e1c
Transaction hash: 0x125e4bc5251af8ee2664ea0d1495b36c593f25f78f1a78f637a3f7aafa9e22
````
Burada yeni kontratınızın adresini görebilirsiniz. 
Kontratla etkileşimde bulunmak için bu adrese ihtiyacınız olacak.

- Aşağıdaki gibi environment değişkenini ayarlamalısınız:
````bash
# The deployment address of the previous contract.
export CONTRACT_ADDRESS="<address of the previous contract>"
````
### Kontrat ile Etkileşim
- boost_balance() çağırmak için aşağıdaki komutu çalıştırmalısınız: 
````bash
starknet invoke \
    --address ${CONTRACT_ADDRESS} \
    --abi first_contract_abi.json \
    --function increase_balance \
    --inputs 1234
	````
Örnek output:
````bash
Invoke transaction was sent.
Contract address: 0x039564c4f6d9f45a963a6dc8cf32737f0d51a08e446304626173fd838bd70e1c
Transaction hash: 0x69d743891f69d758928e163eff1e3d7256752f549f134974d4aa8d26d5d7da8
````
- Aşağıdaki komut, sahip olduğunuz transaction hash'e dayalı olarak transaction durumunu sorgulamanıza izin verir (burada TRANSACTION_HASH'ı starknet invoke tarafından yazdırılan transaction hash ile değiştirmeniz gerekiyor):
````bash
starknet tx_status --hash TRANSACTION_HASH
````
Örnek output:
````bash
{
    "block_hash": "0x0",
    "tx_status": "ACCEPTED_ON_L2"
}
````
- *Olası outputlar: *

1. **NOT_RECEIVED:** Transaction henüz alınmadı (yani depolamaya yazılmadı).
1. **RECEIVED:** Transaction sıralayıcı tarafından alındı.
1. **PENDING:** The transaction doğrulamayı geçti ve bekleyen bloğa girdi.
1. **REJECTED:** Transaction doğrulamada başarısız oldu ve bu nedenle atlandı.
1. **ACCEPTED_ON_L2:** Transaction, doğrulamayı geçti ve gerçek olarak oluşturulmuş bir bloğa girdi.
1. **ACCEPTED_ON_L1:** Transaction , zincir üzerinde kabul edildi.

### Bakiyeyi Sorgulama
Güncel bakiyeyi sorgulamak için kullanmanız gereken komut: 
````bash
starknet call \
    --address ${CONTRACT_ADDRESS} \
    --abi first_contract_abi.json \
    --function get_balance
	````
Output: 

````bash
1234```

Güncel bakiyeyi görmek için bakiye artırım transaction durumunun en az ACCEPTED_ON_L2 (yani, ACCEPTED_ON_L2 veya ACCEPTED_ON_L1) olmasını beklemeniz gerektiğini unutmamalısınız. Aksi takdirde bakiyeyi increase_balance işlemi yapılmadan önce (yani 0) bakiyeyi görürsünüz.

