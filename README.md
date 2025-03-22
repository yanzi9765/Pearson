The Pearson correlation coefficient (named for Karl Pearson) can be used to summarize the strength of the linear relationship between two data samples.

The Pearson’s correlation coefficient is calculated as the covariance of the two variables divided by the product of the standard deviation of each data sample. It is the normalization of the covariance between the two variables to give an interpretable score.

Pearson's correlation coefficient = covariance(X, Y) / (stdv(X) * stdv(Y))

The use of mean and standard deviation in the calculation suggests the need for the two data samples to have a Gaussian or Gaussian-like distribution.

We discuss here the possibility of using Pearson correlation coefficients integrated into a finite rationality hypothesis model to classify user characteristics as a means of filtering out the factors that influence differences in user needs and behaviors to be used as a basis for user classification.



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
