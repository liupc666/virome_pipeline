```text
work_dir/
├── cleandata/          # fastp clean fq
├── bowtie2_hr/         # bowtie2 去宿主后的非宿主 fq
├── contig_megahit/     # megahit 组装结果
├── genomad/
│   ├── ${sample}/      # genomad 原始输出
│   └── checkv/
│       └── ${sample}/  # checkv end_to_end 输出
├── vs2/
│   ├── ${sample}/      # vs2 原始输出
│   └── checkv/
│       └── ${sample}/  # checkv end_to_end 输出
└── votu/
    ├── ${sample}_vcontigs.fna   # 每个样本的病毒序列输出（vs2 和 genomad 识别的序列）
    ├── all_vcontigs.fna         # 所有样本的病毒序列输出
    ├── votu_raw.fna             # cd-hit 聚类结果
    └── votu.fna                 # vOTU 重命名后的结果
```


1.viral_identify使用说明 \
新建工作目录./ \
确保./rawdata下存放原始双端数据，格式：${sample}_1.fq.gz和${sample}_2.fq.gz \
确保存在样本名文件./sample_name.txt，每行为样本名 \
多样本并行作业需修改第6行#SBATCH --array参数 \
在工作目录下，sbatch ~/scripts/pipeline/vir_identify.sh \
最终在votu文件夹中生存每个样本的候选病毒序列，${sample}_vcontigs.fna


2.vir_clustering使用说明 \
在上述工作目录下运行，该脚本将自动合并./votu下的所有“样本名_vcontigs.fna”，生成“all_vcontigs.fna”，\
进一步使用cd-hit对all_vcontigs.fna进行聚类生成votu_raw.fna， \
进一步对votu从vOTU_0001开始重命名，生产votu.fna \
