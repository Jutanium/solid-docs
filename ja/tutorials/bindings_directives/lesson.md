Solid は `use:` 名前空間を通じてカスタムディレクティブをサポートしています。これは単なる `ref` のシンタックスシュガーですが、典型的なバインディングに似ており、同じ要素に複数のバインディングがあっても衝突しないという点で有用です。これにより、再利用可能な DOM 要素の動作のための優れたツールになります。

カスタムディレクティブは、`(element, valueAccesor)` という形式のシンプルな関数で、`valueAccessor` はバインディングの値を取得する関数です。この関数がスコープ内にインポートされる限り、`use:` で使用できます。

> 重要: `use:` は変換されるコンパイラによって検出され、関数はスコープ内にあることが要求されるため、スプレッドの一部にしたり、コンポーネントに適用することはできません。

この例では、ポップアップやモーダルを閉じるための「外側をクリックした時の動作」のシンプルなラッパーを作成しています。まず、要素に `clickOutside` ディレクティブをインポートして使用する必要があります。

```jsx
<div class="modal" use:clickOutside={() => setShow(false)}>
  Some Modal
</div>
```

`click-outside.tsx` を開き、ここでカスタムディレクティブを定義します。このディレクティブは、body にバインドして、時間になったらクリーンアップするクリックハンドラーを定義します。

```jsx
export default function clickOutside(el, accessor) {
  const onClick = (e) => !el.contains(e.target) && accessor()?.();
  document.body.addEventListener("click", onClick);

  onCleanup(() => document.body.removeEventListener("click", onClick));
}
```

これでモーダルを交互に開いたり閉じたりできるようになります。
