---
Title | Tools Conda anaconda2miniforge
-- | --
Created @ | `2024-06-22T17:16:36Z`
Updated @| `2024-06-22T17:16:36Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/309)

---
# Anaconda -> Miniforge
- Anaconda 为公司运营，收费的，鉴于某些原因，一些企业转移到社区开发的 miniforge


---
- Anaconda 和 Miniconda 是 anaconda 公司的产品，商用是付费的，个人暂时免费
- Miniforge 是由社区主导，用 GitHub 托管，完全免费
- Mambaforge 已经不再维护

> As of September 2023, the new usage of Mambaforge is thus discouraged. Bug reports specific to Mambaforge will be closed as won't fix

## Steps

- Install [minifoge](https://conda-forge.org/miniforge/)
- ~~Move `anaconda envs` to `miniforge`~~

```
mv ~/anaconda3/envs/* ~/miniforge3/envs/
```
> [!CAUTION]
> envs 下之前的目录包含很多 anaconda3/miniconda3 的内容，不能很好的迁移



- config the conda environments.txt
```
sed -i 's/anaconda3/miniforge3/g' ~/.conda/environments.txt
```

- config the conda envs in `.bashrc`
```
sed -i 's/anaconda3/miniforge3/g' ~/.bashrc
```
- remove the anaconda channels 

```
sed -i '/defaults/d' ~/.condarc
```

- remove the anaconda

```
rm -fr ~/anaconda3
```

- restart shell




