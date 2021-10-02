O repositório remoto é um servidor aonde são armazenados e controlados apenas as alterações, ou seja, é um repositório puro.<br>
Para criar um repositório remoto, utilizamos o comando `git remote` seguido de `add` e o nome que será dado e o caminho, podendo ser uma URL, uma pasta específica, ou qualquer endereço válido.
```
$ git remote add nome-repositorio caminho/para/o/repositorio
```
Apenas o comando `git remote -v`, lista os repositórios remotos e seus endereços, tanto para fetch (busca) quando para push (empurrar).
