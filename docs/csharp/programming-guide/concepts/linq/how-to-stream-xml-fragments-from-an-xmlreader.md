---
title: Como transmitir fragmentos XML de um XmlReader (C#)
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 4a8f0e45-768a-42e2-bc5f-68bdf0e0a726
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 84b2c4f9726a552fa60cc68266c418b25dbf0408
ms.contentlocale: pt-br
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-stream-xml-fragments-from-an-xmlreader-c"></a>Como transmitir fragmentos XML de um XmlReader (C#)
Quando você tem que processa grandes arquivos XML, talvez não seja possível carregar a árvore inteira XML na memória. Este tópico mostra como passar informações usando <xref:System.Xml.XmlReader>.  
  
 Um dos modos de efetivas usar <xref:System.Xml.XmlReader> para ler objetos de <xref:System.Xml.Linq.XElement> é escrever seu próprio método personalizado do eixo. Um método do eixo normalmente retorna uma coleção como <xref:System.Collections.Generic.IEnumerable%601> de <xref:System.Xml.Linq.XElement>, conforme mostrado no exemplo neste tópico. No método personalizado do eixo, depois de criar o fragmento XML chamando o método <xref:System.Xml.Linq.XNode.ReadFrom%2A> , retornar a coleção usando `yield return`. Isso fornece a semântica de execução adiada ao método personalizado do eixo.  
  
 Quando você cria uma árvore XML de um objeto de <xref:System.Xml.XmlReader> , <xref:System.Xml.XmlReader> deve ser posicionado em um elemento. O método de <xref:System.Xml.Linq.XNode.ReadFrom%2A> não retorna até que lê a marca do elemento.  
  
 Se você desejar criar uma árvore parcial, você pode criar uma instância <xref:System.Xml.XmlReader>, posiciona o leitor no nó que você deseja converter a <xref:System.Xml.Linq.XElement> uma árvore e em seguida, cria o objeto de <xref:System.Xml.Linq.XElement> .  
  
 O tópico [Como transmitir fragmentos XML com acesso a informações de cabeçalho (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-stream-xml-fragments-with-access-to-header-information.md) contém informações e um exemplo de como transmitir um documento mais complexo.  
  
 O tópico [Como executar a transformação de streaming de grandes documentos XML (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-perform-streaming-transform-of-large-xml-documents.md) contém um exemplo do uso de LINQ to XML para transformar documentos XML muito grandes, mantendo uma pegada de memória pequena.  
  
## <a name="example"></a>Exemplo  
 Este exemplo cria um método personalizado do eixo. Você pode consultá-lo usando uma consulta [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]. O método de eixo personalizado `StreamRootChildDoc` é um método que foi projetado especificamente para ler um documento que tenha um elemento `Child` de repetição.  
  
```csharp  
static IEnumerable<XElement> StreamRootChildDoc(StringReader stringReader)  
{  
    using (XmlReader reader = XmlReader.Create(stringReader))  
    {  
        reader.MoveToContent();  
        // Parse the file and display each of the nodes.  
        while (reader.Read())  
        {  
            switch (reader.NodeType)  
            {  
                case XmlNodeType.Element:  
                    if (reader.Name == "Child") {  
                        XElement el = XElement.ReadFrom(reader) as XElement;  
                        if (el != null)  
                            yield return el;  
                    }  
                    break;  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    string markup = @"<Root>  
      <Child Key=""01"">  
        <GrandChild>aaa</GrandChild>  
      </Child>  
      <Child Key=""02"">  
        <GrandChild>bbb</GrandChild>  
      </Child>  
      <Child Key=""03"">  
        <GrandChild>ccc</GrandChild>  
      </Child>  
    </Root>";  
  
    IEnumerable<string> grandChildData =  
        from el in StreamRootChildDoc(new StringReader(markup))  
        where (int)el.Attribute("Key") > 1  
        select (string)el.Element("GrandChild");  
  
    foreach (string str in grandChildData) {  
        Console.WriteLine(str);  
    }  
}  
```  
  
 Este exemplo gera a seguinte saída:  
  
```  
bbb  
ccc  
```  
  
 Nesse exemplo, o documento de origem é muito pequeno. No entanto, mesmo se houver milhões de elementos de `Child` , este exemplo ainda terá uma pegada pequena de memória.  
  
## <a name="see-also"></a>Consulte também  
 [Analisando XML (C#)](../../../../csharp/programming-guide/concepts/linq/parsing-xml.md)

