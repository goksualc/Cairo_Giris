
## Hesap Açma

### Ağı Kurmak
Bu bölümde, StarkNet ile etkileşim kurmak için StarkNet CLI'yi (command line interface) kullanacağız. CLI'ye StarkNet testnet ile çalışması talimatını vermek için her komuta --network=alpha-goerli işaretini ekleyebilir veya STARKNET_NETWORK ortam değişkenini aşağıdaki gibi ayarlayabilirsiniz:

````bash
export STARKNET_NETWORK=alpha-goerli
````
### Bir Cüzdan Sağlayıcı Seçme

Externally Owned Accounts (EOA) ile sözleşmeler arasında ayrım yapan Ethereum'un aksine, StarkNet'in böyle ayrımı yoktur. Bunun yerine, bir hesap, hesabın mantığını tanımlayan dağıtılmış bir sözleşme ile temsil edilir - özellikle de ondan kimin işlem düzenleyebileceğini kontrol eden imza şeması.

StarkNet ile etkileşime geçmek için bir hesap sözleşmesi yapmanız gerekecek. Bu öğreticide, OpenZeppelin'in EOA sözleşmesi standardının biraz değiştirilmiş bir sürümünü kullanacağız (şu anda imza farklı şekilde hesaplanmaktadır). STARKNET_WALLET ortam değişkenini aşağıdaki gibi ayarlayın:

````bash
export STARKNET_WALLET=starkware.starknet.wallets.open_zeppelin.OpenZeppelinAccount
````

### Hesap Oluşturma
Aşağıdaki komutu bir hesap açmak için kullanın:

````bash
starknet new_account
````
Örnek output: 
````bash
Account address: 0x004779736196b61f69e7280068de7bb2683ea85084ad02bfb240db20e781b51b
Public key: ...
Move the appropriate amount of funds to the account, and then deploy the account
by invoking the 'starknet deploy_account' command.

NOTE: This is a modified version of the OpenZeppelin account contract. The signature is computed
differently.
````

### Goerli ETH'nin Hesaba Transferi
Hesabı dağıtmak ve StarkNet'te işlem yapmak için gereken ücretleri ödemek için L2 hesabınızda yeterli ETH'ye ihtiyacınız var.

L2 ETH'yi aşağıdaki şekillerde edinebilirsiniz:

- Az önce oluşturduğunuz hesaba doğrudan küçük miktarlarda ETH almak için StarkNet Faucet'i kullanın. Basit işlemler için bu yeterli olacaktır.
- Mevcut Goerli L1 ETH'nizi L2 hesabına ve hesabından aktarmak için StarkGate – StarkNet L2 köprüsünü (L1 sözleşmesi / Web Uygulaması) kullanın.

Hesabı dağıtmak için gereken ücreti tahmin etmek için aşağıdaki komutu çalıştırın:

````bash
starknet deploy_account --simulate
````
Örnek output: 
````bash
The estimated fee is: 822400000000000 WEI (0.000822 ETH).
Gas usage: 8224
Gas price: 100000000000 WEI
````

> Ayrıca alternatif olarak aşağıdaki komutu da uygulayabilirsiniz:

````bash
starknet deploy_account --estimate_fee
````
### Hesabı Deploy Etmek

Yukarıda açtığımız hesabı deploy ediyoruz: 
````bash
starknet deploy_account
````

Örnek output:
````bash
Sent deploy account contract transaction.

Contract address: ...
Transaction hash: ...
````



