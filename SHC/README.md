# UnSHc
UnSHc - Como descriptografar SHc *.sh.x arquivo criptografado?

# Por favor, note
Eu não vou descriptografar nenhum arquivo para as pessoas. Problemas no GitHub são apenas para discutir sobre bug e / ou melhoria da ferramenta "UnSHc".

Devido aos muitos problemas desde shc 4.0.3, parece haver uma necessidade de esclarecimento. No shc 4.0.3 muitas mudanças estruturais foram incorporadas, de modo que o shc agora faz uso de vários mecanismos de segurança fornecidos pelo próprio linux-kernel. Portanto, agora é quase impossível extrair o shell script original com a versão atual do UnSHc, se a nova versão shc foi usada. Isso requer uma abordagem mais aprofundada, o que significa que um bash modificado ou um linux-kernel modificado é necessário para ignorar as medidas de segurança.

Se você acha que encontrou um bug, por favor, forneça-me o arquivo criptografado E o arquivo não criptografado correspondente. Sem esses dois arquivos eu não posso revertê-lo e analisá-lo. Adicione algumas informações sobre a arquitetura onde o arquivo criptografado foi criado (qual distribuição e versão do linux, qual arquitetura x86 ou x64, etc.).

Todos os outros "problemas de descriptografia de arquivos" serão fechados diretamente.

# Revisão SHc
SHc (compilador SHell) é uma ferramenta fabulosa criada e mantida por Francisco Javier Rosales Garcia (http://www.datsi.fi.upm.es/~frosal/). Essa ferramenta protege qualquer shell script com criptografia (ARC4).

wget -q http://www.datsi.fi.upm.es/~frosal/sources/shc-3.8.9.tgz

OU

wget -q https://github.com/srSPEEDiness/Criptografia/raw/main/SHC/shc-3.8.9.tgz

tar zxvf shc-3.8.9b.tgz
cd shc-3.8.9
make test
make

Como usar o SHc?
root@server:~/shc/shc-3.8.9# shc -h
shc Version 3.8.9, Generic Script Compiler
shc Copyright (c) 1994-2012 Francisco Rosales <frosal@fi.upm.es>
shc Usage: shc [-e date] [-m addr] [-i iopt] [-x cmnd] [-l lopt] [-rvDTCAh] -f script
-e %s Expiration date in dd/mm/yyyy format [none]
-m %s Message to display upon expiration [&quot;Please contact your provider&quot;]
-f %s File name of the script to compile
-i %s Inline option for the shell interpreter i.e: -e
-x %s eXec command, as a printf format i.e: exec('%s',@ARGV);
-l %s Last shell option i.e: --
-r Relax security. Make a redistributable binary
-v Verbose compilation
-D Switch ON debug exec calls [OFF]
-T Allow binary to be traceable [no]
-C Display license and exit
-A Display abstract and exit
-h Display help and exit
Environment variables used:
Name Default Usage
CC cc C compiler command
CFLAGS C compiler flags
Please consult the shc(1) man page.
O shell script criptografado é chamado de "*.sh.x" por padrão.

UnSHc é uma ferramenta para reverter a criptografia de qualquer script *.sh.x criptografado SHc.

# Como usar o UnSHc?
[root@server:~/unshc]$ ./unshc.sh -h
 _   _       _____ _   _
| | | |     /  ___| | | |
| | | |_ __ \ `--.| |_| | ___
| | | | '_ \ `--. \  _  |/ __|
| |_| | | | /\__/ / | | | (__
 \___/|_| |_\____/\_| |_/\___|

--- UnSHc - The shc decrypter.
--- Version: 0.6
------------------------------
UnSHc is used to decrypt script encrypted with SHc
Original idea from Luiz Octavio Duarte (LOD)
Updated and modernized by Yann CAM
- SHc   : [http://www.datsi.fi.upm.es/~frosal/]
- UnSHc : [https://www.asafety.fr/unshc-the-shc-decrypter/]
------------------------------

[*] Usage : ./unshc.sh [OPTIONS] <file.sh.x>
         -h | --help                          : print this help message
         -a OFFSET | --arc4 OFFSET            : specify the arc4() offset arbitrarily (without 0x prefix)
         -d DUMPFILE | --dumpfile DUMPFILE    : provide an object dump file (objdump -D script.sh.x > DUMPFILE)
         -s STRFILE | --stringfile STRFILE    : provide a string dump file (objdump -s script.sh.x > STRFILE)
         -o OUTFILE | --outputfile OUTFILE    : indicate the output file name

[*] e.g :
        ./unshc.sh script.sh.x
        ./unshc.sh script.sh.x -o script_decrypted.sh
        ./unshc.sh script.sh.x -a 400f9b
        ./unshc.sh script.sh.x -d /tmp/dumpfile -s /tmp/strfile
        ./unshc.sh script.sh.x -a 400f9b -d /tmp/dumpfile -s /tmp/strfile -o script_decrypted.sh
UnSHc só pode descriptografar o arquivo criptografado SHc na arquitetura X86/x64.

Demonstração em vídeo :
https://www.youtube.com/watch?v=tmHVhMuG-Vg
SHc (em francês) :
https://www.asafety.fr/prog-and-dev/bashshunix-shc-le-compilateur-et-protecteur-de-script-shell/
UnSHc (em francês) :
https://www.asafety.fr/unshc-the-shc-decrypter/
# UnSHc-MIPS
Graças ao @fffonion, uma versão dedicada do UnSHc foi lançada visando o arquivo criptografado SHc na arquitetura MIPS. Esta versão do UnSHc-MIPS está disponível aqui: https://github.com/fffonion/UnSHc-MIPS

Obrigado mais uma vez pelo vosso trabalho e contribuição!

# UnSHc-ARM
Graças ao @cliffalbert, uma versão dedicada do UnSHc foi lançada visando o arquivo criptografado SHc na arquitetura ARM. Esta versão do UnSHc-ARM está disponível aqui : https://github.com/cliffalbert/UnSHc-arm

Obrigado mais uma vez pelo vosso trabalho e contribuição!