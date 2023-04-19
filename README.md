# upsource
fixed upsource for jetbrains 2023.1 IDEs

Basically ButtonlessScrollBarUI.getTrackBackgroundDefault() was deprecated quite a long time ago, and it seems it was finally removed in 2023.1 versions.
I monkeypatched the ModernCommentLabel class file by replacing this call with a new JBColor(0,0) by editing the bytecode from this:

```
INVOKEDYNAMIC produce ()Lcom/intellij/util/NotNullProducer; ${H_META} args[()Ljava/lang/Object;, handle[H_INVOKESTATIC com/intellij/util/ui/ButtonlessScrollBarUI.getTrackBackgroundDefault()Lcom/intellij/ui/JBColor;], ()Ljava/awt/Color;]
INVOKESPECIAL com/intellij/ui/JBColor.<init>(Lcom/intellij/util/NotNullProducer;)V
```

to this:

```
ICONST_0
ICONST_0
INVOKESPECIAL com/intellij/ui/JBColor.<init>(II)V
```

It's been a long time since I used java, and I never really worked directly with the bytecode, but this works for me, so it should for you too.
