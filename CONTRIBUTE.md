
# How to Contribute Guide

We use the final result from Hermez phase 1 ceremony for Perptual Powers of Tau with 54 contributions as the basis for Railgun phase 1. The setup is outlined here: https://ipfs.io/ipfs/QmYft5k2sY6KJ5V3hkw7FZmHLM7k33uMvwzQy9yC1gt8mF

Since Railgun circuits have relatively smaller numbers of constraints less than 2^19, we use a truncated smaller file [pot19.ptau](https://mesquka-nextcloud20.cp01.cloudboxes.io/s/DERF4GLW7CQYpbS) with b2sum 
````
bca9d8b0 4242f175 189872c4 2ceaa21e
2951e0f0 f272a0cc 54fc3719 3ff66486
00eaf1c5 55c70cde dfaf9fb7 4927de7a
a1d33dc1 e2a7f1a5 06194849 89da0887
````

## Requirements

In this tutorial, I'll describe all the steps required to run them on your own hardware.

The important part of the ceremony is that the toxic value is not leaked and it's deleted after the completion of the ceremony.

This toxic value is in the memory while the ceremony is running. This toxic value is not displayed anywhere and it's not stored anywhere. It's recomended to restart the machine after the ceremony is completed to be sure this toxic value is not accessible any more.

## Preparation of the Machine.

You will need nodejs version at least v14.

Quick instructions to install node if you don't have it:

````
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
source ~/.bashrc
nvm install v14.8.0
node --version
````

Install snarkjs:

````bash
npm install -g snarkjs@0.3.59
````

At the begining of your contribution you will receive two files:

* `small_xxxx.zkey`  (150MB)
* `large_xxxx.zkey` (255MB)

Where `xxxx` is the contribution of the last participant.


Take note of the blake2b of the inputs and check with the ceremony coordinator the integrity of the files:
````bash
b2sum small_xxxx.zkey.zkey
b2sum large_xxxx.zkey.zkey
````

To contribute you need to run:

````bash
snarkjs zkey contribute small_xxxx.zkey small_yyyy.zkey -n=yourName -e="smash the keyboard for some long random text"
````

Substitute `yourName` for the name you want to appear in the file. Please do not uses spaces or special characters so we don't have problems.  This name is important because this is what will be displayed, together with the contribution hash when all the contributions are listed in the final zkey file verification.

Substitute also `yyyy` by the actual contrubution.  This should be `xxxx` + 1.

For `-e` value in the command, write a long random text by simply smashing the keyboard.

Write down the Circuit Hash and the Contribution Hash printed at the end.

The circuit hash for the small circuit must be:

````
323539fd 42268d6d 90ff822b 4cede1dd
7ac028d8 c4830783 50bc63f7 493890ec
e97c1b8d 8dbe25fc ab9757db e9bc6c59
3d2c6331 a20ae546 f18fe3a4 81c6006b
````

This Hash is computed at the phase two preparation, and depends on the r1cs file and the Powers of Tau result ceremony. More detail about verification can be found in [Verify.md](VERIFY.md)

Repeat the steps above for `large` circuit.

````bash
snarkjs zkey contribute large_xxxx.zkey large_yyyy.zkey -n=yourName -e="for the second time, smash the keyboard for some long random text"
````

The circuit hash for `large` must be:

````
449c7a56 44d78d1d aa168105 2750971a
41d57569 7080945d 32e249c5 679c819b
bb8942d9 902bf76e 9767759d 89f9a19e
8eaf22f6 c5ef965f 1525befc 9ed574a4
````

Write down the contribution hash for both circuits.

Now you can compute the checksum of your contribution results.

````bash
b2sum small_yyyy.zkey
b2sum large_yyyy.zkey
````

With this, you will have all the information to fill the attestation template.

Create a copy of the [template_attestation.md](template_attestation.md) with name `yyyy_yourName_attestation`

Fill all the fields of the template.

Sign the template with your PGP Keybase.

And generate a signed attestation with name:
`yyyy_yourName_attestation_signed`


Send the 2 responses plus the signed attestation to the coordinator.

Send also a link to yout PGP keybase to the coordinator.

Thank you very much for contributing!
