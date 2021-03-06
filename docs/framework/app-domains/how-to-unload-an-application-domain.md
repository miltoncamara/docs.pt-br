---
title: "Como descarregar um domínio de aplicativo | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unload method
- application domains, unloading
- unloading application domains
ms.assetid: f356116d-e415-4f7c-a332-6e6a60227192
caps.latest.revision: 10
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: b9146d7565809cc0f92556478f93b9d444538826
ms.contentlocale: pt-br
ms.lasthandoff: 06/02/2017

---
# <a name="how-to-unload-an-application-domain"></a>Como descarregar um domínio de aplicativo
Quando terminar de usar um domínio do aplicativo, descarregue-o usando o método <xref:System.AppDomain.Unload%2A?displayProperty=fullName>. O método **Unload** desliga normalmente o domínio de aplicativo especificado. Durante o processo de descarga, nenhum thread novo pode acessar o domínio do aplicativo e todas as estruturas de dados específicas do domínio do aplicativo são liberadas.  
  
 Os assemblies carregados no domínio do aplicativo são removidos e não ficam mais disponíveis. Se um assembly no domínio do aplicativo forem independentes de domínio, os dados para o assembly permanecerão na memória até que todo o processo seja desligado. Não há outro mecanismo para descarregar um assembly com neutralidade de domínio a não ser desligar o processo inteiro. Há situações em que a solicitação para descarregar um domínio do aplicativo não funciona e resulta em uma <xref:System.CannotUnloadAppDomainException>.  
  
 O exemplo a seguir cria um novo domínio do aplicativo chamado `MyDomain`, imprime algumas informações no console e descarrega o domínio do aplicativo. Observe que o código tenta imprimir o nome amigável do domínio do aplicativo descarregado no console. Essa ação gera uma exceção que é manipulada pelas instruções try/catch no fim do programa.  
  
## <a name="example"></a>Exemplo  
 [!code-cpp[System.AppDomain.Load#3](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.appdomain.load/cpp/source3.cpp#3)] [!code-csharp[System.AppDomain.Load#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.load/cs/source3.cs#3)] [!code-vb[System.AppDomain.Load#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.load/vb/source3.vb#3)]  
  
## <a name="see-also"></a>Consulte também  
 [Programação com domínios do aplicativo](http://msdn.microsoft.com/en-us/bd36055b-56bd-43eb-b4d8-820c37172131)   
 [Como criar um domínio do aplicativo](../../../docs/framework/app-domains/how-to-create-an-application-domain.md)   
 [Uso de domínios do aplicativo](../../../docs/framework/app-domains/use.md)
