## O que é o Patch-Package?

O **patch-package** é uma ferramenta que permite modificar dependências instaladas no projeto sem alterar diretamente os arquivos no diretório `node_modules`. Isso é especialmente útil no Strapi quando você precisa ajustar uma dependência para atender a requisitos específicos.

---

## Por Que Usar Patch-Package no Strapi?

Ao trabalhar com o Strapi, pode surgir a necessidade de:

- Ajustar o comportamento de bibliotecas de terceiros.
    
- Corrigir erros temporários em dependências sem esperar por uma atualização oficial.
    
- Aplicar modificações específicas que não estão disponíveis nas configurações padrão.
    

Usar o `patch-package` garante que essas alterações sejam preservadas mesmo após reinstalar as dependências com `npm install` ou `yarn install`.

---

## Como Funciona o Patch-Package?

### Passos Básicos:

1. **Instalação:** Instale o `patch-package` no seu projeto.
    
2. **Modificação:** Altere diretamente os arquivos dentro de `node_modules`.
    
3. **Gerar o Patch:** Crie o patch para salvar as mudanças.
    
4. **Aplicação:** O patch será reaplicado automaticamente toda vez que as dependências forem reinstaladas.
    

---

## Configuração no Projeto Strapi

### 1. Instalar o Patch-Package

Execute o seguinte comando no terminal:

```
npm install patch-package --save-dev
```

Ou, se estiver usando Yarn:

```
yarn add patch-package --dev
```

### 2. Ajustar o Script no `package.json`

Adicione o script `postinstall` para garantir que os patches sejam aplicados após cada instalação:

```
"scripts": {
  "postinstall": "patch-package"
}
```

### 3. Realizar Alterações nas Dependências

- Localize o arquivo a ser modificado dentro de `node_modules`.
    
- Edite o arquivo conforme necessário.
    

Por exemplo, se você deseja ajustar um método em uma dependência:

```
// Antes
function example() {
  console.log('Original');
}

// Depois
function example() {
  console.log('Modificado!');
}
```

### 4. Gerar o Arquivo de Patch

Após realizar as alterações, gere o patch com o seguinte comando:

```
npx patch-package nome-da-dependencia
```

Isso criará um arquivo `.patch` no diretório `patches/` do seu projeto.

### 5. Validar a Aplicação do Patch

Para confirmar que o patch foi aplicado corretamente:

1. Remova a pasta `node_modules`.
    
2. Reinstale as dependências com `npm install` ou `yarn install`.
    
3. Verifique se as alterações estão presentes.
    

---

## Exemplo de Uso com o Strapi

### Cenário:

Você quer modificar a biblioteca `@strapi/plugin-users-permissions` para adicionar uma nova regra de autenticação.

#### Passos:

1. Localize o arquivo da regra em `node_modules/@strapi/plugin-users-permissions/some-file.js`.
    
2. Faça as alterações desejadas no arquivo.
    
3. Gere o patch:
    
    ```
    npx patch-package @strapi/plugin-users-permissions
    ```
    
4. O patch será salvo em `patches/@strapi+plugin-users-permissions.patch`.
    
5. Execute `npm install` ou `yarn install` para validar.
    

---

## Boas Práticas

1. **Documente as Alterações:**
    
    - Sempre anote o motivo e os detalhes das mudanças para referência futura.
        
2. **Evite Dependências Desnecessárias:**
    
    - Use patches apenas quando não há alternativa, como substituir uma biblioteca ou aguardar atualizações oficiais.
        
3. **Integração com Controle de Versão:**
    
    - Certifique-se de versionar a pasta `patches/` no Git para que outros desenvolvedores apliquem os patches automaticamente.
        
4. **Teste Após Alterações:**
    
    - Sempre valide que o patch funciona conforme esperado e não causa efeitos colaterais.
        

---

## Solução de Problemas

1. **Erro ao Aplicar Patches:**
    
    - Certifique-se de que a versão da dependência corresponde à usada para criar o patch.
        
2. **Patches Não Aplicados Após Instalação:**
    
    - Verifique o script `postinstall` no `package.json`.
        
3. **Conflitos com Atualizações:**
    
    - Atualize a dependência e recrie o patch, se necessário.
        

---

## Resumo

O `patch-package` é uma solução poderosa para ajustar dependências do Strapi sem comprometer a integridade do projeto. Com ele, é possível personalizar o comportamento de bibliotecas e corrigir problemas específicos enquanto mantém um fluxo de trabalho organizado e eficiente.