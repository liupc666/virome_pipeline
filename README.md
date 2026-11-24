1.viral_identify使用说明 \
新建工作目录./ \
确保./rawdata下存放原始双端数据，格式：样本名_1.fq.gz和样本名_2.fq.gz \
确保存在样本名文件./sample_name.txt，每行为样本名 \
多样本并行作业需修改第6行#SBATCH --array参数 \
在工作目录下，sbatch ~/scripts/pipeline/vir_identify.sh \
最终在votu文件夹中生存每个样本的候选病毒序列，样本名_vcontigs.fna


2.vir_clustering使用说明 \
在上述工作目录下运行，该脚本将自动合并./votu下的所有“样本名_vcontigs.fna”，生成“all_vcontigs.fna”，\
进一步使用cd-hit对all_vcontigs.fna进行聚类生成votu_raw.fna， \
进一步对votu从vOTU_0001开始重命名，生产votu.fna \
