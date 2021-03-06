---
title: Trabalhando com logs de aplicativo no Visual Basic
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- logs, application
- application event logs, Visual Basic
- application event logs
ms.assetid: 2581afd1-5791-4bc4-86b2-46244e9fe468
caps.latest.revision: 21
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0f6916571ff978c6558343ff51217b5d342a4d5c
ms.contentlocale: pt-br
ms.lasthandoff: 07/28/2017

---
# <a name="working-with-application-logs-in-visual-basic"></a>Trabalhando com logs de aplicativo no Visual Basic
Os objetos `My.Applicaton.Log` e `My.Log` facilitam a gravação de informações de registro em log e rastreamento em logs.  
  
## <a name="how-messages-are-logged"></a>Como as mensagens são registradas em log  
 Primeiro, a gravidade da mensagem é verificada com a propriedade <xref:System.Diagnostics.TraceSource.Switch%2A> da propriedade <xref:Microsoft.VisualBasic.Logging.Log.TraceSource%2A> do log. Por padrão, somente mensagens com gravidade "Information" e superior são passadas para os ouvintes de rastreamento, especificados na coleção `TraceListener` do log. Em seguida, cada ouvinte compara a gravidade da mensagem com a propriedade <xref:System.Diagnostics.TraceSource.Switch%2A> do ouvinte. Se a gravidade da mensagem for alta o suficiente, o ouvinte gravará a mensagem.  
  
 O diagrama a seguir mostra como uma mensagem gravada no método `WriteEntry` é passada para os métodos `WriteLine` dos ouvintes de rastreamento do log:  
  
 ![Minha chamada de log](../../../../visual-basic/developing-apps/programming/log-info/media/mylogcall.png "MyLogCall")  
  
 É possível alterar o comportamento do log e dos ouvintes de rastreamento alterando o arquivo de configuração do aplicativo. O diagrama a seguir mostra a correspondência entre as partes do log e o arquivo de configuração.  
  
 ![Minha configuração de log](../../../../visual-basic/developing-apps/programming/log-info/media/mylogconfig.png "MyLogConfig")  
  
## <a name="where-messages-are-logged"></a>Onde as mensagens são registradas em log  
 Se o assembly não tiver nenhum arquivo de configuração, os objetos `My.Application.Log` e `My.Log` serão gravados na saída de depuração do aplicativo (por meio da classe <xref:System.Diagnostics.DefaultTraceListener>). Além disso, o objeto `My.Application.Log` é gravado no arquivo de log do assembly (por meio da classe <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener>), enquanto o objeto `My.Log` é gravado na saída da página da Web do ASP.NET (por meio da classe <xref:System.Web.WebPageTraceListener>).  
  
 A saída de depuração pode ser vista na janela [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)]**Saída** ao executar o aplicativo no modo de depuração. Para abrir a janela **Saída**, clique no item de menu **Depuração**, aponte para **Janelas** e, em seguida, clique em **Saída**. Na janela **Saída**, selecione **Depuração** na caixa **Mostrar saída de**.  
  
 Por padrão, `My.Application.Log` grava o arquivo de log no caminho para os dados de aplicativo do usuário. Você pode obter o caminho pela propriedade <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.FullLogFileName%2A> do objeto <xref:Microsoft.VisualBasic.Logging.Log.DefaultFileLogWriter%2A>. O formato do caminho é o seguinte:  
  
 `BasePath`\\`CompanyName`\\`ProductName`\\`ProductVersion`  
  
 Um valor típico para `BasePath` é o seguinte.  
  
 C:\Documents and Settings\\`username`\Application Data  
  
 Os valores de `CompanyName`, `ProductName` e `ProductVersion` vêm das informações do assembly do aplicativo. O formato do nome do arquivo de log é *AssemblyName*.log, em que *AssemblyName* é o nome do arquivo do assembly sem a extensão. Se mais de um arquivo de log for necessário, como quando o log original não está disponível quando o aplicativo tenta gravar no log, o formato do nome do arquivo de log será *AssemblyName*-*iteration*.log, em que `iteration` é um `Integer` positivo.  
  
 Você pode substituir o comportamento padrão adicionando ou alterando os arquivos de configuração de aplicativo e do computador. Para obter mais informações, consulte [Instruções passo a passo: Alterando onde My.Application.Log grava informações](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md).  
  
## <a name="configuring-log-settings"></a>Definindo configurações de log  
 O objeto `Log` tem uma implementação padrão que funciona sem um arquivo de configuração do aplicativo, app.config. Para alterar os padrões, você precisa adicionar um arquivo de configuração com as novas configurações. Para obter mais informações, consulte [Instruções passo a passo: filtrando a saída de My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md).  
  
 As seções de configuração de log ficam localizadas no nó `<system.diagnostics>` no nó `<configuration>` principal do arquivo app.config. As informações de log são definidas em vários nós:  
  
-   Os ouvintes para o objeto `Log` são definidos no nó `<sources>` chamado DefaultSource.  
  
-   O filtro de gravidade para o objeto `Log` é definido no nó `<switches>` chamado DefaultSwitch.  
  
-   Os ouvintes de log são definidos no nó `<sharedListeners>`.  
  
 Exemplos dos nós `<sources>`, `<switches>` e `<sharedListeners>` são mostrados no código a seguir:  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="DefaultSource" switchName="DefaultSwitch">  
        <listeners>  
          <add name="FileLog"/>  
        </listeners>  
      </source>  
    </sources>  
    <switches>  
      <add name="DefaultSwitch" value="Information" />  
    </switches>  
    <sharedListeners>  
      <add name="FileLog"  
        type="Microsoft.VisualBasic.Logging.FileLogTraceListener,  
          Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral,   
          PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL"  
        initializeData="FileLogWriter"  
      />  
    </sharedListeners>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="changing-log-settings-after-deployment"></a>Alterando configurações de log após a implantação  
 Quando você desenvolve um aplicativo, suas configurações são armazenadas no arquivo app.config, conforme mostrado nos exemplos acima. Após implantar o aplicativo, você ainda pode configurar o log editando o arquivo de configuração. Em um aplicativo baseado no Windows, o nome do arquivo é *applicationName*.exe.config e ele deve residir na mesma pasta que o arquivo executável. Para um aplicativo Web, este é o arquivo Web.config associado ao projeto.  
  
 Quando seu aplicativo executa o código que cria uma instância de uma classe pela primeira vez, ele verifica o arquivo de configuração para obter informações sobre o objeto. Para o objeto `Log`, isso ocorre na primeira vez em que o objeto `Log` é acessado. O sistema examina o arquivo de configuração apenas uma vez para qualquer objeto em particular – na primeira vez em que seu aplicativo cria o objeto. Portanto, talvez seja necessário reiniciar o aplicativo para que as alterações entrem em vigor.  
  
 Em um aplicativo implantado, você habilita o código de rastreamento reconfigurando objetos de opção antes de iniciar seu aplicativo. Normalmente, isso envolve ativar e desativar os objetos de opção ou alterar os níveis de rastreamento e, então, reiniciar o aplicativo.  
  
## <a name="security-considerations"></a>Considerações sobre segurança  
 Considere o seguinte ao gravar dados no log:  
  
-   **Evite vazar informações do usuário.** Certifique-se de que seu aplicativo grave somente informações aprovadas no log. Por exemplo, pode ser aceitável que o log do aplicativo contenha nomes de usuário, mas não senhas.  
  
-   **Proteja os locais do log.** Qualquer log que contiver informações possivelmente confidenciais deve ser armazenado em um local seguro.  
  
-   **Evite informações enganosas.** Em geral, seu aplicativo deve validar todos os dados inseridos por um usuário antes de usar esses dados. Isso inclui gravar dados no log do aplicativo.  
  
-   **Evite situações de negação de serviço.** Se seu aplicativo gravar muitas informações no log, ele poderá encher o log ou tornar difícil de encontrar informações importantes.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 [Registrando informações em log no aplicativo](../../../../visual-basic/developing-apps/programming/log-info/logging-information-from-the-application.md)

