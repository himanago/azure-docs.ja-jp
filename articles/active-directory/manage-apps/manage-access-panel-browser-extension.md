---
title: IE 用 Azure アクセス パネル拡張機能のトラブルシューティング | Microsoft Docs
description: グループ ポリシーを使用してマイ アプリ ポータル用の Internet Explorer アドオンをデプロイする方法。
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/11/2018
ms.author: barbkess
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ebd949460f826c9529b9f392bc4a7f4918ee170
ms.sourcegitcommit: c29d7ef9065f960c3079660b139dd6a8348576ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "44715042"
---
# <a name="troubleshooting-the-access-panel-extension-for-internet-explorer"></a>Internet Explorer 用アクセス パネル拡張機能のトラブルシューティング
この記事は、次の問題をトラブルシューティングする際に役立ちます。

* Internet Explorer を使用中にマイ アプリ ポータルからアプリにアクセスできない。
* ソフトウェアをインストール済みでも "ソフトウェアをインストールしてください" というメッセージが表示される。

管理者の方は、「 [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](deploy-access-panel-browser-extension.md)

## <a name="run-the-diagnostic-tool"></a>診断ツールの実行
アクセス パネルの診断ツールをダウンロードし実行することで、アクセス パネル拡張機能のインストールに関する問題を診断することができます。

1. [ここをクリックして診断ツールをダウンロードします。](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. ファイルを開いて **[すべて展開]** クリックします。
   
    ![Press Extract All](./media/manage-access-panel-browser-extension/extract1.png)
3. **[展開]** をクリックして続行します。
   
    ![Press Extract](./media/manage-access-panel-browser-extension/extract2.png)
4. **AccessPanelExtensionDiagnosticTool** という名前のファイルを右クリックし、**[プログラムから開く] > [Microsoft Windows Based Script Host]** の順にクリックしてツールを実行します。
   
    ![[プログラムから開く] > [Microsoft Windows Based Script Host]](./media/manage-access-panel-browser-extension/open_tool.png)
5. インストールの問題点を示す次の診断ウィンドウが表示されます。
   
    ![A sample of the diagnostic window](./media/manage-access-panel-browser-extension/tool_preview.png)
6. **[はい]** をクリックして、見つかった問題をプログラムに修正させます。
7. 変更内容を保存するために、すべての Internet Explorer ウィンドウを閉じてから再び Internet Explorer を開きます。<br />まだアプリにアクセスできない場合は、次の手順をお試しください。

## <a name="check-that-the-access-panel-extension-is-enabled"></a>アクセス パネル拡張機能が有効になっていることを確認する
Internet Explorer でアクセス パネル拡張機能が有効になっていることを確認するには:

1. Internet Explorer で、ウィンドウの右上隅にある **歯車アイコン**をクリックします。 次に、**[インターネット オプション]** を選択します <br />(古いバージョンの Internet Explorer では、**[ツール] > [インターネット オプション]** の順にクリックします)。
   
    ![Go to Tools > Internet Options](./media/manage-access-panel-browser-extension/internetoptions.png)
2. **[プログラム]** タブをクリックして、**[アドオンの管理]** をクリックします。
   
    ![Click Manage Add-Ons](./media/manage-access-panel-browser-extension/internetoptions_programs.png)
3. このダイアログで、**[アクセス パネル拡張機能]** を選択して **[有効にする]** ボタンをクリックします。
   
    ![Click Enable](./media/manage-access-panel-browser-extension/enableaddon.png)
4. 変更内容を保存するために、すべての Internet Explorer ウィンドウを閉じてから再び Internet Explorer を開きます。

## <a name="enable-extensions-for-inprivate-browsing"></a>InPrivate ブラウズで拡張機能を有効にする
InPrivate ブラウズ モードを使用している場合:

1. Internet Explorer で、ウィンドウの右上隅にある **歯車アイコン**をクリックします。 次に、**[インターネット オプション]** を選択します <br />(古いバージョンの Internet Explorer では、**[ツール] > [インターネット オプション]** の順にクリックします)。
   
    ![A sample of the diagnostic window](./media/manage-access-panel-browser-extension/inprivateoptions.png)
2. **[プライバシー]** タブに移動し、**[InPrivate ブラウズの開始時に、ツール バーと拡張機能を無効にする]** チェック ボックスを**オフ**にします。</p>
   
    ![Uncheck Disable toolbars and extensions when InPrivate Browsing starts](./media/manage-access-panel-browser-extension/enabletoolbars.png)
3. 変更内容を保存するために、すべての Internet Explorer ウィンドウを閉じてから再び Internet Explorer を開きます。

## <a name="uninstall-the-access-panel-extension"></a>アクセス パネル拡張機能のアンインストール
コンピューターからアクセス パネル拡張機能をアンインストールするには:

1. キーボードの **Windows キー** を押して [スタート] メニューを開きます。 メニューが開いているときに好きな文字を入力して、検索を行うことができます。 「コントロール パネル」と入力して、 **[コントロール パネル]** が検索結果に表示されたらそれを開きます。
   
    ![Search for Control Panel](./media/manage-access-panel-browser-extension/search_sm.png)
2. コントロール パネルの右上隅にある **[表示方法]** を、**[大きいアイコン]** に変更します。 **[プログラムと機能]** を見つけてクリックします。
   
    ![Chang the view to show Large Icons](./media/manage-access-panel-browser-extension/control_panel.png)
3. リストから **[アクセス パネル拡張機能]** を選択し、**[アンインストール]** をクリックします。
   
    ![Click Uninstall](./media/manage-access-panel-browser-extension/uninstall.png)
4. 拡張機能をもう一度インストールして、問題が解決されたかどうかを確認することができます。

拡張機能のアンインストールで問題が発生する場合は、 [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) ツールを使用して削除することも可能です。

## <a name="related-articles"></a>関連記事
* [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](what-is-single-sign-on.md)
* [グループ ポリシーを使用して Internet Explorer 用アクセス パネル拡張機能をデプロイする方法](deploy-access-panel-browser-extension.md)

