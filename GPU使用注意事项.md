1、注意模型、损失函数、数据都要放到GPU上

```python
device = torch.device("cuda:0")
net.to(device)
function.to(decive)
inputs.to(device)
labels.to(device)
```

2、多GPU使用

```python
if torch.cuda.is_available():
    device = torch.device("cuda")
    os.environ["CUDA_DEVICE_ORDER"] = "PCI_BUS_ID"
    os.environ["CUDA_VISIBLE_DEVICES"] = "0,1,2,3"
    device_ids = [0, 1, 2, 3]
    net = nn.DataParallel(net,device_ids = device_ids)
    net.to(device)
```

