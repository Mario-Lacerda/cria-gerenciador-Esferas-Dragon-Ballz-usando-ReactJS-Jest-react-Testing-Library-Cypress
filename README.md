
# Desafio Dio - Crie um Gerenciador de Esferas do Dragon BallZ Usando ReactJS, Jest, React Testing Library e Cypress



**Projeto abrangente para criar um Gerenciador de Esferas do Dragon BallZ usando ReactJS, Jest, React Testing Library e Cypress**



Este projeto visa criar um Gerenciador de Esferas do Dragon BallZ usando ReactJS, Jest, React Testing Library e Cypress. O objetivo é construir um aplicativo funcional e testável que permita aos usuários gerenciar suas esferas do Dragon BallZ.



### **Requisitos**

- Conhecimento de ReactJS

- Conhecimento de Jest

- Conhecimento de React Testing Library

- Conhecimento de Cypress

- Node.js e npm instalados

  

### **Etapas**



#### **1. Configuração do projeto**

- Crie um novo projeto ReactJS usando `npx create-react-app gerenciador-esferas-dbz`.

- Instale as dependências necessárias:

  - `npm install --save jest react-testing-library cypress`

    

#### **2. Criando o componente Esfera**

- Crie um componente `Esfera.js` para representar uma esfera do Dragon BallZ.

- Este componente deve incluir propriedades para o nome, descrição e status da esfera.

  

#### **3. Criando o componente Gerenciador de Esferas**

- Crie um componente `GerenciadorDeEsferas.js` para gerenciar as esferas do Dragon BallZ.

- Este componente deve incluir métodos para adicionar, remover e atualizar esferas.

  

#### **4. Testando os componentes**

- Use Jest e React Testing Library para testar os componentes `Esfera` e `GerenciadorDeEsferas`.
- Crie testes para verificar o comportamento esperado desses componentes.



#### **5. Testando o aplicativo**

- Use Cypress para testar o aplicativo como um todo.
- Crie testes para verificar o fluxo de usuário e a funcionalidade geral do aplicativo.



### **Códigos**

Aqui estão alguns códigos de exemplo que você pode usar para este projeto:



### **Componente Esfera**

javascript



```javascript
import React from "react";

const Esfera = ({ nome, descricao, status }) => {
  return (
    <div>
      <h2>{nome}</h2>
      <p>{descricao}</p>
      <p>{status}</p>
    </div>
  );
};

export default Esfera;
```



### **Componente Gerenciador de Esferas**

javascript



```javascript
import React, { useState } from "react";
import Esfera from "./Esfera";

const GerenciadorDeEsferas = () => {
  const [esferas, setEsferas] = useState([]);

  const adicionarEsfera = (nome, descricao, status) => {
    setEsferas([...esferas, { nome, descricao, status }]);
  };

  const removerEsfera = (nome) => {
    setEsferas(esferas.filter((esfera) => esfera.nome !== nome));
  };

  const atualizarEsfera = (nome, descricao, status) => {
    setEsferas(esferas.map((esfera) => esfera.nome === nome ? { ...esfera, descricao, status } : esfera));
  };

  return (
    <div>
      {esferas.map((esfera) => (
        <Esfera key={esfera.nome} {...esfera} />
      ))}
      <button onClick={() => adicionarEsfera("Esfera do Dragão", "Esfera mágica que concede desejos.", "Ativa")}>Adicionar Esfera</button>
      <button onClick={() => removerEsfera("Esfera do Dragão")}>Remover Esfera</button>
      <button onClick={() => atualizarEsfera("Esfera do Dragão", "Esfera mágica que concede desejos.", "Inativa")}>Atualizar Esfera</button>
    </div>
  );
};

export default GerenciadorDeEsferas;
```



### **Testes de Jest**

javascript



```javascript
import React from "react";
import { render, fireEvent } from "@testing-library/react";
import Esfera from "./Esfera";
import GerenciadorDeEsferas from "./GerenciadorDeEsferas";

describe("Componente Esfera", () => {
  it("deve renderizar o nome, descrição e status da esfera", () => {
    const { getByText } = render(<Esfera nome="Esfera do Dragão" descricao="Esfera mágica que concede desejos." status="Ativa" />);
    expect(getByText("Esfera do Dragão")).toBeInTheDocument();
    expect(getByText("Esfera mágica que concede desejos.")).toBeInTheDocument();
    expect(getByText("Ativa")).toBeInTheDocument();
  });
});

describe("Componente Gerenciador de Esferas", () => {
  it("deve adicionar uma nova esfera quando o botão 'Adicionar Esfera' é clicado", () => {
    const { getByText, getByRole } = render(<GerenciadorDeEsferas />);
    fireEvent.click(getByRole("button", { name: /Adicionar Esfera/i }));
    expect(getByText("Esfera do Dragão")).toBeInTheDocument();
  });

  it("deve remover uma esfera quando o botão 'Remover Esfera' é clicado", () => {
    const { getByText, getByRole } = render(<GerenciadorDeEsferas />);
    fireEvent.click(getByRole("button", { name: /Adicionar Esfera/i }));
    fireEvent.click(getByRole("button", { name: /Remover Esfera/i }));
    expect(getByText("Esfera do Dragão")).not.toBeInTheDocument();
  });

  it("deve atualizar uma esfera quando o botão 'Atualizar Esfera' é clicado", () => {
    const { getByText, getByRole } = render(<GerenciadorDeEsferas />);
    fireEvent.click(getByRole("button", { name: /Adicionar Esfera/i }));
    fireEvent.click(getByRole("button", { name: /Atualizar Esfera/i }));
    expect(getByText("Esfera do Dragão")).toHaveTextContent("Inativa");
  });
});
```



### **Testes de Cypress**

javascript



```javascript
describe("Gerenciador de Esferas do Dragon BallZ", () => {
  beforeEach(() => {
    cy.visit("/");
  });

  it("deve adicionar uma nova esfera", () => {
    cy.get("button[name=Adicionar Esfera]").click();
    cy.contains("Esfera do Dragão").should("be.visible");
  });

  it("deve remover uma esfera", () => {
    cy.get("button[name=Adicionar Esfera]").click();
    cy.get("button[name=Remover Esfera]").click();
    cy.contains("Esfera do Dragão").should("not.exist");
  });

  it("deve atualizar uma esfera", () => {
    cy.get("button[name=Adicionar Esfera]").click();
    cy.get("button[name=Atualizar Esfera]").click();
    cy.contains("Esfera do Dragão").should("have.text", "Inativa");
  });
});
```



## **Conclusão**



Este projeto fornece um guia passo a passo e códigos para criar um Gerenciador de Esferas do Dragon BallZ usando ReactJS, Jest, React Testing Library e Cypress. Ao integrar essas tecnologias em seu fluxo de trabalho, você pode criar aplicativos ReactJS robustos e testáveis com confiança.
