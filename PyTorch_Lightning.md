当前项目中主要使用，[PyTorch Lightning](https://lightning.ai/docs/pytorch/stable/) 框架，在此进行记录

==暂未进行章节区分==

## Lightning Module

在继承 `pl.LightningModule` 构建自己的 net 时，需要记住框架在真正运行时，会运行的那些步骤，及其顺序，并针对性地进行覆写

以下示例中，看函数名字，就能知道运行顺序，详细情况还是查官方文档[Callback — PyTorch Lightning](https://lightning.ai/docs/pytorch/stable/extensions/callbacks.html#callback)

```python
"""运行顺序
for epoch_i in range(num_epoch):

    on_train_epoch_start()
    for batch in trainning_dataloader:
    	on_train_batch_start()
        trainning_step()
        on_train_batch_end()
    on_train_epoch_end()
    
    
    on_validation_start()
	for batch in validation_dataloader:
		on_validation_batch_start()
        validation_step()
        on_validation_batch_end
    on_validation_end()
	
"""



class CustomNet(pl.LightningModule):
    def __init__(self, options: dict):
        super().__init__()
        self.save_hyperparameters()
        self._options = VqVaePartttenNetHyperParameters.parse_obj(options)
        self._lr = self._options.learning_rate
		...

    def configure_optimizers(self):
        optimizer = torch.optim.AdamW(self.parameters(), lr=self._lr)
        return {
            "optimizer": optimizer,
            "lr_scheduler": {
                "scheduler": torch.optim.lr_scheduler.MultiStepLR(
                    optimizer, milestones=[30, 60], gamma=0.1
                ),
                "frequency": 1,
                "interval": "epoch",
                "strict": True,
                "name": "learning_rate",
            },
        }

    def forward(
        self,
        seq_daliy_industry_lv1_mean: torch.Tensor,
        seq_intraday: Optional[torch.Tensor] = None,
    ) -> torch.Tensor:
		...
       

        return nearest_neighbor, preds

    def training_step(self, batch, batch_idx):
        ...

        return loss

    def validation_step(self, batch, batch_idx):
        ...


    def on_train_epoch_start(self) -> None:
      	...

    def on_train_epoch_end(self) -> None:
        ...
        
    def on_validation_epoch_start(self) -> None:
     	...

    def on_validation_epoch_end(self) -> None:
       	...

```



## [sanity_checking](https://lightning.ai/docs/pytorch/stable/common/trainer.html#sanity-checking)

在正式的训练之前（指 `training_step` `validation_step`) 运行前，会进行检查，`self.trainer.sanity_checking` 判断是否处于此状态，以对一些 hooks 进行屏蔽，以下为示例：

```python
def on_train_epoch_end(self) -> None:
    result = self._signal_analysis_cache_train.compute()
    if self.trainer.sanity_checking:
        entropy = torch.tensor(0.0)
    else:
        counts = torch.bincount(self.zq_indices_train, minlength=32)
        probs = counts.float() / self.zq_indices_train.shape[0]
        entropy = -(probs * torch.log2(probs + 1e-9)).sum()
```

