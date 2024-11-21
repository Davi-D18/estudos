# Tutorial: Configuração e Uso do `react-router-dom` 
no React  O **React Router** é uma biblioteca essencial para criar navegação em aplicações React. Ele permite que você crie várias páginas (ou "rotas") de forma eficiente, sem recarregar a página inteira.  

 ## **1. Configurando o `react-router-dom` no projeto**  
 ### **Passo 1: Instalar o React Router** No terminal, execute o seguinte comando para instalar a biblioteca:  
 
 ```bash 
 npm install react-router-dom
 ```

### **Passo 2: Verificar compatibilidade**

Certifique-se de que está usando **React 18 ou superior**, pois a API do React Router foi ajustada para esta versão.

---

## **2. Entendendo os principais conceitos**

- **BrowserRouter**: Envolve toda a aplicação, fornecendo o contexto necessário para gerenciar rotas.
- **Routes**: Contêiner onde todas as rotas são definidas.
- **Route**: Define uma rota específica, associando um caminho (`path`) a um componente.
- **Link**: Substitui a tag `<a>` para navegação interna, evitando o recarregamento da página.
- **useNavigate**: Um hook para navegação programática (mudar de página via código).
- **useParams**: Hook para acessar parâmetros dinâmicos da URL.

---

## **3. Implementando rotas no React**

### **Estrutura inicial do projeto**

Vamos criar uma aplicação com três páginas:

- **Home**: Página inicial.
- **About**: Informações sobre o site.
- **Contact**: Página de contato.

### **Passo 1: Criar os componentes das páginas**

Organize os componentes das páginas em uma pasta chamada `src/pages`. Exemplo de código para cada página:

```jsx
// src/pages/Home.jsx 
export const Home = () => {   
	return <h1>Bem-vindo à página inicial!</h1>; 
}; 
// src/pages/About.jsx 
export const About = () => {   
	return <h1>Sobre nós</h1>; 
}; 

// src/pages/Contact.jsx 
export const Contact = () => {   
	return <h1>Fale conosco</h1>; 
}; 
```

---

### **Passo 2: Configurar as rotas no `App.jsx`**

Edite o arquivo `src/App.jsx` para incluir o React Router:
```jsx
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import Home from './pages/Home';
import About from './pages/About';
import Contact from './pages/Contact';

export const App = () => {
  return (
    <Router>
      <nav>
        <a href="/">Home</a> | <a href="/about">About</a> | <a href="/contact">Contact</a>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </Router>
  );
};

```

---

### **Passo 3: Navegação com o componente `<Link>`**

Substitua os links `<a>` pelo componente `<Link>` do React Router para evitar o recarregamento da página:

```jsx
import { Link } from 'react-router-dom';

export const App = () => {
  return (
    <Router>
      <nav>
        <Link to="/">Home</Link> | <Link to="/about">About</Link> | <Link to="/contact">Contact</Link>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </Router>
  );
};

```

---

### **Passo 4: Navegação programática com `useNavigate`**

O React Router permite navegação via código usando o hook `useNavigate`:

```jsx
import { useNavigate } from 'react-router-dom';

export const Home = () => {
  const navigate = useNavigate();

  const goToContact = () => {
    navigate('/contact');
  };

  return (
    <div>
      <h1>Bem-vindo à página inicial!</h1>
      <button onClick={goToContact}>Ir para contato</button>
    </div>
  );
};

```
---

### **Passo 5: Rotas dinâmicas com parâmetros**

Para criar rotas que aceitam parâmetros na URL, use o `:paramName` no `path`:

```jsx
<Route path="/product/:id" element={<Product />} />
```

No componente, utilize o hook `useParams` para acessar os parâmetros da URL:

```jsx
import { useParams } from 'react-router-dom';

export const Product = () => {
  const { id } = useParams();
  return <h1>Produto: {id}</h1>;
};

```

---

## **4. Adicionando recursos extras**

### **Rota padrão para páginas inexistentes**

Inclua uma rota `*` para capturar URLs inválidas:

```jsx
<Route path="*" element={<h1>Página não encontrada!</h1>} />
```

---

## **5. Estruturando o projeto**

Uma boa organização para projetos React com rotas seria:

```css
src/
│
├── pages/
│   ├── Home.jsx
│   ├── About.jsx
│   └── Contact.jsx
│
├── App.jsx
└── index.jsx

```

# Outra Abordagem
## **Configuração no `main.jsx` com `createBrowserRouter`**

```jsx
// main.jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { RouterProvider, createBrowserRouter } from 'react-router-dom';
import Home from './pages/Home';
import About from './pages/About';
import Contact from './pages/Contact';

const routes = createBrowserRouter([
  {
    path: '/',
    element: <Home />,
  },
  {
    path: '/about',
    element: <About />,
  },
  {
    path: '/contact',
    element: <Contact />,
  },
  {
    path: '*',
    element: <h1>Página não encontrada!</h1>, // Rota para páginas inexistentes
  },
]);

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <RouterProvider router={routes} />
  </React.StrictMode>
);

```

---

A função `createBrowserRouter` cria um roteador baseado no navegador e aceita um **array de rotas**. Cada rota no array pode incluir as seguintes propriedades:

- **`path`**: Define o caminho da URL que ativa a rota.
    
    - Exemplo: `"/about"` será ativado em `https://example.com/about`.
- **`element`**: O componente renderizado quando a rota correspondente é acessada.
    
    - Exemplo: `element: <Home />`.
- **`children`** _(opcional)_: Permite definir **sub-rotas** dentro de uma rota principal.
    
    - Exemplo: `/products` pode ter sub-rotas como `/products/:id`.
- **`errorElement`** _(opcional)_: Componente renderizado quando ocorre um erro na rota.
    
    - Exemplo: Página personalizada para rotas inexistentes.
- **Rotas dinâmicas**:
    
    - `path` pode conter parâmetros dinâmicos, como `:id` ou `:slug`, para rotas que variam de acordo com o contexto.
    - Exemplo: Uma rota como `/products/:id` renderiza um produto específico.

---

### **`RouterProvider`**

- Substitui o tradicional `BrowserRouter` do React Router.
- Recebe o roteador criado com o `createBrowserRouter` como prop.
- Conecta o roteador à aplicação, permitindo que os componentes reajam às mudanças na URL.

---

## **Estrutura do projeto**

A estrutura do projeto com essa abordagem seria algo como:

```css
src/
│
├── pages/
│   ├── Home.jsx
│   ├── About.jsx
│   └── Contact.jsx
│
├── main.jsx
└── index.html

```

---

## **Vantagens dessa abordagem**

1. **Organização centralizada das rotas:**
    
    - Todas as rotas estão declaradas em um único lugar, o que facilita a manutenção.
2. **Escalabilidade:**
    
    - Para projetos maiores, você pode definir sub-rotas ou agrupar rotas relacionadas em um único objeto.
3. **Customização:**
    
    - É mais fácil adicionar propriedades adicionais às rotas, como autenticação.


## **Exemplo Completo com Rotas Específicas**

Aqui está um exemplo funcional com:

1. **Rota Principal (`/`)**.
2. **Rota Inexistente (`*`)**.
3. **Rotas Dinâmicas (`/products/:id`)**.

### **Código: `main.jsx`**

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { createBrowserRouter, RouterProvider } from 'react-router-dom';
import Home from './pages/Home';
import About from './pages/About';
import Contact from './pages/Contact';
import Product from './pages/Product';
import ErrorPage from './pages/ErrorPage';

// Configurando as rotas
const routes = createBrowserRouter([
  { 
	path: '/', element: <Home /> 
  },
  { 
	path: '/about', element: <About /> 
  },
  { 
	path: '/contact', element: <Contact /> 
  },
  {
    path: '/products/:id',
    element: <Product />,
  },
  {
    path: '*',
    element: <ErrorPage />, // Página para rotas inexistentes
  },
]);

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <RouterProvider router={routes} />
  </React.StrictMode>
);

```

---

### **Exemplo de Páginas**

#### **`ErrorPage.jsx`**

Página personalizada para rotas inexistentes.

```jsx
export const ErrorPage = () => {
  return (
    <div>
      <h1>404 - Página não encontrada!</h1>
      <p>Desculpe, a página que você tentou acessar não existe.</p>
    </div>
  );
};

```

---

#### **`Product.jsx`**

Página que utiliza parâmetros dinâmicos na rota.

```jsx
import { useParams } from 'react-router-dom';

export const Product = () => {
  const { id } = useParams(); // Extrai o parâmetro dinâmico da URL

  return (
    <div>
      <h1>Detalhes do Produto</h1>
      <p>ID do Produto: {id}</p>
    </div>
  );
};

```

---

### **Como Testar**

1. **Página Inicial (`/`)**:
    
    - URL: `http://localhost:3000/`
    - Componente: `<Home />`.
2. **Rota Dinâmica (`/products/:id`)**:
    
    - URL: `http://localhost:3000/products/42`.
    - Componente: `<Product />` exibirá `ID do Produto: 42`.
3. **Rota Inexistente (`*`)**:
    
    - URL: `http://localhost:3000/qualquer-coisa`.
    - Componente: `<ErrorPage />`.

---

## **Vantagens dessa Abordagem**

1. **Centralização e Organização:**
    
    - Todas as rotas estão bem definidas em um único local (`main.jsx`).
2. **Rotas Dinâmicas:**
    
    - Fácil implementação de rotas com parâmetros, como `:id`.
3. **Tratamento de Erros:**
    
    - Permite definir uma página de erro global para rotas inexistentes.
4. **Escalabilidade:**
    
    - Ideal para projetos maiores, com suporte a sub-rotas e middleware.
5. **Flexibilidade:**
    
    - Customização de rotas com propriedades adicionais, como autenticação ou permissões futuras.