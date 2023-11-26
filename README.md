# Padrões e técnicas avançadas com Git e Github
## Padrões de branch
![](https://github.com/PedroGuilhermeSilv/full-cycle/blob/main/aulas/git-github/img/gitflow.png)

1. Branches Principais:
    - main: Representa a linha principal de desenvolvimento e contém apenas código estável e testado.
    - develop: É o ramo de integração, onde as contribuições individuais são mescladas antes de serem lançadas.
    ```
    # Cria feature
    git checkout develop
    # Vai para branch main
    git checkout main    
    # Mergea as atualizações
    git merge develop
    ```

2. Branches de Feature (Funcionalidade):
    - feature/{nome-da-feature}: Criados a partir do ramo develop para desenvolver novas funcionalidades. Após a conclusão, são mesclados de volta para develop.
    ```
    # Cria feature
    git checkout -b feature/{nome-da-feature}
    # Vai para branch develop
    git checkout develop
    # Mergea as atualizações
    git merge feature/{nome-da-feature}
    # excluir um branch local
    git branch -d feature/{nome-da-feature}
    # excluir um branch remoto
    git push origin --delete feature/{nome-da-feature}
    ```


3. Branches de Release (Versão):
    - release/{versão}: Ramo criado a partir de develop quando há recursos suficientes para uma versão. É usado para correções finais e preparação para lançamento. Após testes, é mesclado na main e develop, e uma tag é criada.
    ```
    # Vai para branch develop
    git checkout develop
    # Cria a release
    git checkout -b release/{versão}
    # Vai para branch develop
    git checkout develop
    # Mergea as atualizações
    git merge release/{versão}
    # Vai para branch main
    git checkout main
    # Mergea as atualizações
    git merge release/{versão}
    # Vai para branch release
    git checkout release
    # Crie uma tag
    git tag -a nome_da_tag -m "Mensagem da tag"
    ```

                
4. Branches de Hotfix (Correção Rápida):
    - hotfix/{nome-da-correcao}: Criados a partir de master para corrigir problemas críticos em produção. Assim que a correção é feita, é mesclada em master e develop, e uma tag é criada.


## Trabalhando com assinatura de commits
1. Gerando chave gpg 
```
gpg --full-generate-key

```
2. Ecolha RSA, tamannho de 4096 bits, validade (1y=1 ano, 1m= 1 mês), nome que será o mesmo usando no "git config --global user.name" e seu e-mail.

3. Depois da chave criada execute este comando para copiar sua chave:
```
gpg --list-secret-key --keyid-form LONG

```
copie o id da chave (Ex:rsa4096/{id_chave})

```
gpg --armor --export {id_chave}

```

4. Copie a chave -> vá para seu github -> configurações-> SSH and GPG Keys -> New GPG Key -> cole sua chave.

5. Configure o git local para utilizar a chave gpg nos commits:
```
git config --global user.signingkey {id_chave}

```
6. Force a utilizar a chave gpg nos commits do repositório atual.
```
git config commit.gpgsign true

```
