# Spatial-Temporal Person Re-identification

----------
Code for st-ReID(pytorch). We achieve **Rank@1=98.1%, mAP=87.6%** without re-ranking and **Rank@1=98.0%, mAP=95.5%** with re-ranking for market1501.For Duke-MTMC, we achieve **Rank@1=94.4%, mAP=83.9%** without re-ranking and **Rank@1=94.5%, mAP=92.7%** with re-ranking.

## 1. ST-ReID
### 1.1 model
![](https://i.imgur.com/WYCcBHO.jpg)

### 1.2 result
![](https://i.imgur.com/KubElWp.jpg)
----------

![](https://i.imgur.com/Ul6h45K.jpg)


## 2. rerequisites
- **Pytorch 0.3**
- Python 3.6
- Numpy


## 3. experiment
### Market1501
1. data prepare<br>
   1) change the path of dataset <br>
   2) python3 prepare.py --Market

2. train (appearance feature learning) <br>
python3 train_market.py --PCB --gpu_ids 2 --name ft_ResNet50_pcb_market_e --erasing_p 0.5 --train_all --data_dir "/home/huangpg/st-reid/dataset/market_rename/"

3. test (appearance feature extraction) <br>
python3 test_st_market.py --PCB --gpu_ids 2 --name ft_ResNet50_pcb_market_e --test_dir "/home/huangpg/st-reid/dataset/market_rename/" 

4. generate st model (spatial-temporal distribution) <br>
python3 gen_st_model_market.py --name ft_ResNet50_pcb_market_e --data_dir "/home/huangpg/st-reid/dataset/market_rename/"
5. evaluate (joint metric, you can use your own visual feature or spatial-temporal streams) <br>
python3 evaluate_st.py --name ft_ResNet50_pcb_market_e 

6. re-rank<br>
6.1) python3 gen_rerank_all_scores_mat.py --name ft_ResNet50_pcb_market_e <br>
6.2) python3 evaluate_rerank_market.py --name ft_ResNet50_pcb_market_e


### DukeMTMC-reID
1. data prepare<br>
python3 prepare --Duke

2. train (appearance feature learning) <br>
python3 train_duke.py --PCB --gpu_ids 2 --name ft_ResNet50_pcb_duke_e --erasing_p 0.5 --train_all --data_dir "/home/huangpg/st-reid/dataset/DukeMTMC_prepare/"

3. test (appearance feature extraction) <br>
python3 test_st_duke.py --PCB --gpu_ids 2 --name ft_ResNet50_pcb_duke_e --test_dir "/home/huangpg/st-reid/dataset/DukeMTMC_prepare/" 

4. generate st model (spatial-temporal distribution) <br>
python3 gen_st_model_duke.py --name ft_ResNet50_pcb_duke_e  --data_dir "/home/huangpg/st-reid/dataset/DukeMTMC_prepare/"

5. evaluate (joint metric, you can use your own visual feature or spatial-temporal streams) <br>
python3 evaluate_st.py --name ft_ResNet50_pcb_duke_e 

6. re-rank<br>
6.1) python3 gen_rerank_all_scores_mat.py --name ft_ResNet50_pcb_duke_e <br>
6.2) python3 evaluate_rerank_duke.py --name ft_ResNet50_pcb_duke_e

## Citation

If you use this code, please kindly cite it in your paper.

```latex
@article{guangcong2019aaai,
  title={Spatial-Temporal Person Re-identification},
  author={Wang, Guangcong and Lai, Jianhuang and Huang, Peigen and Xie, Xiaohua},
  booktitle={AAAI},
  year={2019}
}
```

## Related Repos

Our codes are mainly based on this [repository](https://github.com/layumi/Person_reID_baseline_pytorch) 
