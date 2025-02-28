# 概要

[手を動かしてわかるクリーンアーキテクチャ　ヘキサゴナルアーキテクチャによるクリーンなアプリケーション開発](https://book.impress.co.jp/books/1123101096)4章のサンプルプロジェクト構成。

## メモ
adapter/inとport/inの対応関係を1:1で綺麗に整理したいのは理解できるが、port/inのUseCaseとdomain/serviceのServiceをインターフェースと実装の関係にする必然性が理解できない。
訳注にあるように、ドメイン層からポート層への(逆向きの)依存が発生してしまっている。

ポート層のインターフェースとして例えばHanlderを設けて、Handlerが1~2つのUseCaseを保持し使用する作りはどうか？
※このとき、Service implements UseCaseという関係。

```java
// application/port/in/SendMoneyHandler.x
class SendMoneyHandler {
    // application/domain/service/
    //                          SendMoneyUseCase.x     (Interface)
    //                          SendMoneyUseCaseImpl.x (Implementation)
    private final SendMoneyUseCase sendMoneyUseCase;
    
    public Output handle(Params params) {
        return sendMoneyUseCase.run(params);
    }
}
```

訳注のアプリケーションサービスとはどのようなものか？

## 気持ち
4章まで読んだ時点だと、まだ全然 `4.1 層を意識したパッケージ構成` でシンプルにDDD風(?)にやっていくほうが整理がつきやすそう。
本文の例だと、上述の通りport/inがやや破綻しており、あとの判断はout次第。

