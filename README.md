# HHCAd_Client

## requirements

Install the requirements.

```bash
pip install -r requirements.txt
```

## Usage

接口：
1. `HCAd_Client.Setup_Client(endpoint, access_key_id, access_key_secret, instance_name, table_name)`
   
   用于连接服务器

2. `HCAd_Client.insert_matrix(df_expression, df_annotation)`
   
   用于上传数据

3. `HCAd_Client.build_index()`
   
   用于建立索引
   
4. `HCAd_Client.query_cells(conditions)`
   
   用于搜索符合条件的数据，输入字符串，返回符合要求的行的主键组成的`List`。
   
   字符串为逻辑表达式，可以带括号，如：
    ```python
    "donor_age== 47yr && organ ==   Heart && (hcad_name==Heart-Connective Tissue-T cell-CCL5 CST7 || hcad_name==Heart-Musle Tissue-Smooth muscle cell-PPP1R15A JUNB )"
    ```
    > 与关系：`&&`； 或关系：`||`； 非关系： `!`； 等于： `==`； 不等于 `<>`;
    >> 注：正常的空格并不影响，但最好不要再字符串尾部出现多余空格，不然有几率bug
5. `HCAd_Client.get_columnsbycell(rows_to_get,cols_to_get,col_condition)`
   
   根据需要的行和需要的列，返回`pd.Dataframe`;
   
   如果需要返回全部列，则`cols_to_get = None`; 
   
   `col_condition`可以传入一个过滤器（filter),
6. `HCAd_Client.get_column_set(col_to_get, col_condition=None)`
   
   返回所需列的全部无重复元素集合，返回类型为`List`。参数类型同5。`col_condition`为可选参数。
   > *注：col_to_get列表长度必须为1。
7. `HCAd_Client.get_all_rows(cols_to_get=[])`
   
   返回指定列的所有行数据，返回类型为`List`，默认返回所有列。
   
   可选参数`cols_to_get`为所需列列名的`list`。

## ChangeLog

### 2020.09.19 `v1.4.1`

- Bug fixed.

### 2020.09.18 `v1.4`
- 添加get_all_rows方法。如需获取所有行数据请使用该方法，效率更高。
- 更新了get_column_set方法。

### 2020.09.17 `v1.3.1`

- V1.3加入可以由逻辑表达转换为filter的 seq2filter(gene_condition), 表达式的使用方法类似于4.