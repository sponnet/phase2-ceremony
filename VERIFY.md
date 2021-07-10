# Verification of phase-2 ceremony for Railgun

## Install node

First install node with nvm:

````
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
source ~/.bashrc
nvm install v14.8.0
node --version
````

## Install circom

````
npm i -g circom@0.5.38
````

## Prepare the circuits

````
cd ~
git clone --depth 1 --branch 
git clone --depth 1 --branch v0.0.1-phase-2-ceremony https://github.com/Railgun-Privacy/circuits.git
cd circuits
npm install
````

## Compile the circuits

The compilation may take a while.

##### Small circuit
````
circom Small.circom --r1cs
````
##### Large circuit
````
circom Large.circom --r1cs
````

## Verify circuits hash
#### Small circuit
````
b2sum Small.r1cs
````

The result should be:

````
82f09719 5e7bed4c a9a74d54 64d100f1
778da513 eb0c6b70 be834661 c0ec12e2
3b65d30b 801937c6 bd86f0bc b8137e26
16aa36be afe262a1 6bc604b5 4b589b65
````

##### Large circtuit
````
b2sum Large.r1cs
````

The result should be:

````
8a57c787 073bb24e 1ed851b9 c82b8ac0
702d9c78 4a77570b 59fda8a3 9ac4a295
639b1574 a8a9eaab 98cffcaa b9c27016
4d91fd57 e08c9b0e 7f79b743 e9a75505
````

## Install snarkjs

````bash
npm i -g snarkjs@0.3.59
````

## Downloading and verifying powers of Tau

First you will need to download powers Of Tau file for phase-1: (pot19.ptau)[https://mesquka-nextcloud20.cp01.cloudboxes.io/s/DERF4GLW7CQYpbS]


Check the blake2b hash of the powers of Tau:
````bash
b2sum pot19.ptau
````

The result should be:

````
bca9d8b0 4242f175 189872c4 2ceaa21e
2951e0f0 f272a0cc 54fc3719 3ff66486
00eaf1c5 55c70cde dfaf9fb7 4927de7a
a1d33dc1 e2a7f1a5 06194849 89da0887
````

If you are also interested in verifying the full powers of tau ceremony for phase-1, you can check this guide: https://ipfs.io/ipfs/QmYft5k2sY6KJ5V3hkw7FZmHLM7k33uMvwzQy9yC1gt8mF


## Verify the final zkey files

##### Small circuit
````
snarkjs zkv small.r1cs pot19.ptau small_final.zkey -v > verification-result
````

The circuit hash must be:
````
323539fd 42268d6d 90ff822b 4cede1dd
7ac028d8 c4830783 50bc63f7 493890ec
e97c1b8d 8dbe25fc ab9757db e9bc6c59
3d2c6331 a20ae546 f18fe3a4 81c6006b
````

##### Large circuit
````
snarkjs zkv large.r1cs pot19.ptau large_final.zkey -v > verification-large.txt
````

The hash of the circuit must be:
````
449c7a56 44d78d1d aa168105 2750971a
41d57569 7080945d 32e249c5 679c819b
bb8942d9 902bf76e 9767759d 89f9a19e
8eaf22f6 c5ef965f 1525befc 9ed574a4
````

You have to match also the contribution hashes of the participants with attestations they published.

As far as there is a single attestatation you trust, you can considere the ceremony for this circuit safe.

## Phase2 Random beacon verification

You can see also the random beacon of the two circuits is the hash of Ethereum Block 12727000
````
4c742a8b 7160d4cc 58882d7e 7dd11a6 
234d99e7 35d2bc12 512d6564 d1dafddfd
````
#### Make a public post.

If you reach this point, it would be great if you can publish a public post or at least a tweet explaining that you verified the circuits.



