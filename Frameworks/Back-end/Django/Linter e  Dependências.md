Um linter python simples, é o `flake8`
```shell
pip install flake8
```

Depois de instalar, basta rodar o comando:
```shell
flake8
```

Ele irá mostrar os erros no código e mostrará onde

Você pode criar um arquivo de configuração `.flake8`:
```python
[flake8]
exclude = venv # Arquivos / pastas para ignorar
ignore = E501 # Regras que devem ser ignoradas
```

Também devemos organizar as dependências do nosso projeto dentro do padrão e boas práticas. Para isso vamos usar o comando _pip freeze_ e salvar as dependências em um arquivo _requirements.txt_

```bash
pip freeze > requirements.txt
```

Separar dependências de produção e dependências de desenvolvimento também é uma boa prática. Para isso, vamos criar um arquivo _requirements_dev.txt_ apenas com dependências de ambiente de desenvolvimento, como o flake8, por exemplo

_requirements_dev.txt_

```
flake8==7.1.1
mccabe==0.7.0
pycodestyle==2.12.1
pyflakes==3.2.0

```