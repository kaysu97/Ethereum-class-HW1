# Ethereum-class-HW1
1.Please compare hash function and cryptographic hash function and give an example.<br>
Hash function 把訊息或資料壓縮成摘要，使得資料量變小，將資料的格式固定下來。資料經過函式產生雜湊值，而雜湊值就當作是陣列的索引，資料就儲存在這個索引的位置中。雜湊值通常用一個短的隨機字母和數字組成的字串來代表。<br>
Hash function的特性為運算速度快、不可逆性(困難度很高)、可能有衝突(因為hash出來是固定長度，所以還是有極低的可能性有衝突)、Hash值平均分布(隨機)。
而cryptographic hash function為hash function的其中一種，所以具有以上Hash function的特性。相較於non cryptographic hash function，它更具安全性，能防止惡意攻擊。<br>
特性為<br>
-同樣的輸入值會出來同樣的hash值。<br>
-任何訊息或資料輸入都能快速算出hash值。<br>
-單向輸入。<br>
-不同的輸入值不會有同樣的結果。<br>
-Hash值和輸入值完全不一樣，且沒有辦法讓你推導出換算方式。<br>
BLAKE2、SHA-2…為cryptographic hash的一種，其應用為: 數位簽章，訊息鑑別碼…。<br>
但如果在沒有惡意攻擊的狀況下，non cryptographic hash function的速度比cryptographic hash function更快。例如: Seahash為non cryptographic hash function的一種，速度可以是BLAKE2( cryptographic hash的一種)的32倍，而non cryptographic hash的應用有:找出重複值、布隆過濾器…。<br><br>

2.Peter is a noob in cryptocurrency and would like to get some Ethers. First step for him is to have an Ethereum account. He decides to generate an account and manages the wallet himself so he can understand the principles behind. From the class, he knows the account is created by the following steps:<br>
a. Can you print the private/public key with hex string representation? Please give us an example.<br>
程式碼:<br>
`const Wallet = require('ethereumjs-wallet');`<br>
`const keccak256 = require('js-sha3').keccak256;`<br>
`// keypair`<br>
`const wallet = Wallet.generate();`<br>
`// privKey‵<br>
`const privKey = wallet.getPrivateKey();`<br>
‵console.log("privKey:", privKey.toString('hex'));`<br>
‵// pubKey`<br>
`const pubKey = wallet.getPublicKey();`<br>
‵console.log("pubKey:", pubKey.toString('hex'));`<br>
`// address`<br>
`let address = wallet.getAddressString();`<br>
‵console.log("address:", address.toString('hex'));`<br>

結果:<br>
privKey: <br>
f940288c4992ad60fcbe0c255edd0a9ec732682ae55c7bbcb916f013a4556f9a<br>
pubKey: <br>
4a0377e7b6ba767593fb60e75d881635f101d47e84aac9a53c40741bc617216709f170c6d36e9db00100fdcd39bcfef94090990dadd1602ba9c9ec8e8d25d4a8<br>
address: <br>
0xada49a72d1b5593f30eeaed52af9b0f138c418f6<br><br>

b. In addition, if we don’t want to use the getAddressString() to get the address, how can we obtain the address by hashing the public key?<br>
程式碼:<br>
let public_key_hash = keccak256(pubKey)<br>
address = "0x"+public_key_hash.slice(-20);<br>
console.log("address:", address);<br>
結果:<br>
address: 0xf1cdc86c6ab375b56dba<br><br>

c. There is a file called Keystore that is used to encrypt the private key and save in a JSON file. Can you generate a Keystore with the password “nccu”? You can find the details about Keystore below.<br>
指令:<br>
step1: geth account new<br>
Your new account is locked with a password. Please give a password. Do not forget this password.<br>
Passphrase:<br>
Repeat passphrase: <br>
address:{0ac42738d7cfc72f4f49f8f75f5ecfd96346bcaa}<br><br>

step2: geth account list<br>
Account #0: {0ac42738d7cfc72f4f49f8f75f5ecfd96346bcaa} keystore://C:\Users\USER\AppData\Roaming\Ethereum\keystore\UTC--2018-10-17T13-04-02.115459500Z--0ac42738d7cfc72f4f49f8f75f5ecfd96346bcaa<br><br>

step3:start C:\Users\USER\AppData\Roaming\Ethereum\keystore\UTC--2018-10-17T13-04-02.115459500Z--0ac42738d7cfc72f4f49f8f75f5ecfd96346bcaa<br>
結果:<br>
```json
{
	"address": "0ac42738d7cfc72f4f49f8f75f5ecfd96346bcaa",
	"crypto": {
		"cipher": "aes-128-ctr",
		"ciphertext": "57e63f1a37fe1385fc73aa1f38ab42d89b608c6e929d91370d3c2d6f192e7239",
		"cipherparams": {
			"iv": "81f076376efaeac5dee9f8e22de8869c"
		},
		"kdf": "scrypt",
		"kdfparams": {
			"dklen": 32,
			"n": 262144,
			"p": 1,
			"r": 8,
			"salt": "ccd6f7ca01a3a1d42626c8d9d00e0949104c5ab299a02444ee9a91588e0af3af"
		},
		"mac": "b069f1c2337fa121428eb3726e3a5cc6a1f1737e5101b933f1f8d34981661131"
	},
	"id": "edb912c4-4a67-40f6-b9d4-876c0d771c2a",
	"version": 3
}
```


