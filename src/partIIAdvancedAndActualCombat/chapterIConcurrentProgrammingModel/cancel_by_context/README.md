Context
• 根 Context:通过 context.Background () 创建
• 子 Context:context.WithCancel(parentContext) 创建

ctx, cancel := context.WithCancel(context.Background())
• 当前 Context 被取消时,基于他的子子 context 都会被取消
• 接收取消通知 <-ctx.Done()
