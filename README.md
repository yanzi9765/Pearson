import pandas as pd
from scipy.stats import pearsonr

def calculate_pearson(data):
    """
    计算给定数据框中每对数值列之间的Pearson相关系数。
    
    参数:
        data (pd.DataFrame): 包含要分析的数据的DataFrame。
        
    返回:
        pd.DataFrame: 包含所有列对的Pearson相关系数的DataFrame。
    """
    # 使用pandas计算相关矩阵
    pearson_corr_matrix = data.corr(method='pearson')
    
    # 使用scipy.stats计算两列间的Pearson相关系数和P值
    for col1 in data.columns:
        for col2 in data.columns:
            if col1 != col2:
                corr, p_value = pearsonr(data[col1], data[col2])
                print(f"Pearson相关系数 ({col1}, {col2}): {corr}, P值: {p_value}")
    
    return pearson_corr_matrix

if __name__ == "__main__":
    # 示例数据
    data = {'Variable1': [2, 4, 6, 8, 10],
            'Variable2': [1, 3, 2, 5, 7]}
    
    df = pd.DataFrame(data)
    
    # 计算并打印Pearson相关系数
    pearson_corr_matrix = calculate_pearson(df)
    print("Pearson相关系数矩阵:\n", pearson_corr_matrix)
