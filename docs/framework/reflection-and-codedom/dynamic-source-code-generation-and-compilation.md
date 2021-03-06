---
title: "Geração e compilação de código-fonte dinâmico | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Code Document Object Model
- System.CodeDom namespace
- language-independent source code modeling
- CodeDOM
- multiple languages supported by CodeDOM
- source code in multiple languages
- languages, multiple language support by CodeDOM
ms.assetid: d077a3e8-bd81-4bdf-b6a3-323857ea30fb
caps.latest.revision: 15
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 86483858b93f58b22d8c8440baa76d68250745dd
ms.contentlocale: pt-br
ms.lasthandoff: 06/02/2017

---
# <a name="dynamic-source-code-generation-and-compilation"></a>Geração e compilação de código-fonte dinâmico
O .NET Framework inclui um mecanismo chamado CodeDOM (Modelo de Objeto do Documento de Código) que permite aos desenvolvedores de programas que emitem o código-fonte gerar o código-fonte em várias linguagens de programação no tempo de execução com base em um único modelo que representa o código a ser renderizado.  
  
 Para representar o código-fonte, os elementos do CodeDOM são vinculados uns aos outros para formar uma estrutura de dados conhecida como um gráfico CodeDOM, que modela a estrutura de parte do código-fonte.  
  
 O namespace `System.CodeDom` define tipos que podem representam a estrutura lógica do código-fonte, independente de uma linguagem de programação específica. O namespace `System.CodeDom.Compiler` define tipos para gerar código-fonte de gráficos CodeDOM e gerenciar a compilação do código-fonte em linguagens com suporte. Fornecedores de compilador ou desenvolvedores podem estender o conjunto de idiomas com suporte.  
  
 A modelagem de código-fonte independente de linguagem pode ser útil quando um programa precisa gerar código-fonte para um modelo de programa em várias linguagens ou para uma linguagem de destino incerta. Por exemplo, alguns designers usam CodeDOM como uma interface da abstração de linguagem para produzir código-fonte na linguagem de programação correta, caso haja suporte para a linguagem no CodeDOM.  
  
 O .NET Framework inclui geradores e compiladores de código para <xref:Microsoft.CSharp.CSharpCodeProvider>, <xref:Microsoft.JScript.JScriptCodeProvider> e <xref:Microsoft.VisualBasic.VBCodeProvider>.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Usando o CodeDOM](../../../docs/framework/reflection-and-codedom/using-the-codedom.md)  
 Descreve os usos comuns e demonstra como criar um gráfico de objeto simples usando o CodeDOM.  
  
 [Gerando e código-fonte e compilando um programa de um gráfico CodeDOM](../../../docs/framework/reflection-and-codedom/generating-and-compiling-source-code-from-a-codedom-graph.md)  
 Descreve como gerar o código-fonte e compilar o código gerado com um compilador externo usando classes definidas no namespace `System.CodeDom.Compiler`.  
  
 [Como criar um arquivo de documentação XML usando CodeDOM](../../../docs/framework/reflection-and-codedom/how-to-create-an-xml-documentation-file-using-codedom.md)  
 Descreve como usar CodeDOM para gerar código com comentários de documentação XML e compilar o código gerado para que ele cria a saída de documentação XML.  
  
 [Como criar uma classe usando o CodeDOM](../../../docs/framework/reflection-and-codedom/how-to-create-a-class-using-codedom.md)  
 Descreve como usar CodeDOM para gerar uma classe que contém campos, propriedades, um método, um construtor e um ponto de entrada.  
  
## <a name="reference"></a>Referência  
 <xref:System.CodeDom>  
 Define os elementos que representam os elementos de código em linguagens de programação que usam o Common Language Runtime como destino.  
  
 <xref:System.CodeDom.Compiler>  
 Define as interfaces para gerar e compilar o código no tempo de execução.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Referência rápida do CodeDOM](http://msdn.microsoft.com/en-us/c77b8bfd-0a32-4e36-b59a-4f687f32c524)  
 Fornece uma maneira rápida para os desenvolvedores localizarem os elementos do CodeDOM que representam os elementos de código-fonte.
