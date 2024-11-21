# Blockchain
Pract - 5 Transaction Mining
Aim: To create and execute a simple blockchain implementation in JavaScript, using mining to validate and add transactions to the blockchain.

const SHA256 = require('cryptojs/sha256');class transactions {
constructor(fromAdd, toAdd, 
amount) {this.fromAdd =
fromAdd;
this.toAdd = toAdd;
this.amount =
amount;
}
}
class Block {
constructor( timestamp, transactions, previousHash = '') {
this.timestamp = timestamp;
this.transactions = transactions;
this.previousHash = 
previousHash;this.hash = 
this.calculateHash(); this.nonce
= 0 ;
}
calculateHash(){
return SHA256(this.prevHash + this.timestamp +
JSON.stringify(this.transactions)+this.nonce).toString();
}
mineBlock(difficulty){
while(this.hash.substring(0, difficulty) !== Array(difficulty+1).join("0")){
this.nonce++;
this.hash = this.calculateHash();
}
console.log("Block mined:" + this.hash)
}
}
class Blockchain 
{
constructor()
{
this.chain = 
[this.createGenesisBlock()];
this.difficulty = 2;
this.pendingTransc = 
[]; this.miningReward
= 50;
}
createGenesisBlock() {
return new Block("01/01/2017", "Genesis Block", "0");
}
getLatestBlock() {
return this.chain[this.chain.length - 1];
}
minePendingTransc(minerAddress) {
let block = new Block(Date.now(), 
this.pendingTransc);block.previousHash = 
this.getLatestBlock().hash;
block.mineBlock(this.difficulty);
console.log("Block successfully 
mined");this.chain.push(block);
this.pendingTransc = [
new transactions(null, minerAddress, this.miningReward)
];
}
createTransc(transc) {
this.pendingTransc.push(trans
c);
}
getBalance(add) 
{let balance =
0;
for (const block of this.chain) {
for (const trans of 
block.transactions) {if
(trans.fromAdd === add) {
balance -= trans.amount;
}
if (trans.toAdd === add) {
balance += trans.amount;
}
}
}
return balance;
}
isChainValid() {
for (let i = 1; i < this.chain.length; 
i++) {const curBlock =
this.chain[i];
const prevBlock = this.chain[i - 1];
if (curBlock.hash !== 
curBlock.calculateHash()) {return false;
}
if (curBlock.previousHash !== 
prevBlock.hash) {return false;
}
}
return true;
}
}
let masterCoin = new Blockchain();
masterCoin.createTransc(new transactions('Sahil', 'Joshi', 
500));masterCoin.createTransc(new transactions('Joshi', 
'Ved', 600)); masterCoin.createTransc(new
transactions('Ved', 'Thore', 500));
console.log('\nStarting the mining ');
masterCoin.minePendingTransc('Shlesha');
console.log('\nBalance of Shlesha is', masterCoin.getBalance('Shlesha'));
console.log('\nStarting the mining ');
masterCoin.minePendingTransc('Shlesha');
console.log('\nBalance of Shlesha is', masterCoin.getBalance('Shlesha'));

