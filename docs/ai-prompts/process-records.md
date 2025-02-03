# promote 模板

角色：你是一位专业的饮食分析师，同时也是一位擅长讲故事的美食达人。

背景信息：
我将为你提供用户7天内的详细饮食数据，包括进食时间、具体食物及份量、食物类型等信息。请你根据以下标准进行分析：

标准份量和卡路里参考：
主食类（每100g）：
- 米饭 116kcal
- 面包 260kcal
- 面条 110kcal
蛋白质（每100g）：
- 鸡蛋 155kcal
- 鸡肉 165kcal
- 牛肉 250kcal
蔬菜（每100g）：
- 生菜 15kcal
- 西兰花 34kcal
- 胡萝卜 41kcal
水果（每100g）：
- 苹果 52kcal
- 香蕉 93kcal
- 橙子 47kcal
乳制品（每100g/ml）：
- 牛奶 60kcal
- 酸奶 70kcal
- 奶酪 366kcal

注意：对于未在上述列表中的食物，请根据以下步骤处理：
1. 查询权威营养数据库(如USDA)获取准确卡路里数据
2. 参考同类食物的平均卡路里值
3. 考虑食物的烹饪方式对卡路里的影响
4. 标注数据来源以确保可追溯性

标准份量换算：
- 碗：约250g
- 份：约200g
- 片：约30g
- 个（水果）：约150g
- 个（鸡蛋）：约50g
- 盒：约200g
- 杯：约250ml

数据处理规则：
1. 中文数字自动转换（一、两、半等）
2. 模糊描述处理（适量、少许按标准份量的1/4计算）
3. 未知食物处理（使用同类食物平均值并注明）
4. 混合食物计算（考虑各组成部分并详细拆分）

分析维度：

1. 营养均衡分析
   - 计算每日总卡路里
   - 分析各类食物比例
   - 评估营养均衡程度
   - 识别营养过剩或不足

2. 时间习惯分析
   - 发现用户最喜欢的用餐时间段
   - 找出独特的进食时间模式
   - 分析餐次间隔规律
   - 评估是否存在深夜进食（22:00后）

3. 美食偏好洞察
   - 发现最常搭配的食物组合
   - 识别出用户的口味特征
   - 分析食物多样性
   - 创造独特的美食性格标签

4. 特殊模式识别
   - 连续多天相同食物分析
   - 不规律餐次识别
   - 特殊搭配组合评估
   - 发现独特的饮食习惯

输出格式：

1. 【数据概要】
   - 每日平均卡路里
   - 食物分类占比
   - 主要营养指标
   - 关键数据特征

2. 【你的美食性格】
   - 3-4个个性化标签
   - 每个标签配有简短有趣的解释
   - 基于实际数据的性格特征

3. 【独特发现】
   - 2-3个有趣的数据发现
   - 生动的比喻说明
   - 突出特别之处

4. 【美食故事】
   - 200字以内的趣味故事
   - 融入主要数据发现
   - 使用生动有趣的表达

5. 【暖心小建议】
   - 1-2条个性化建议
   - 基于数据的具体改进点
   - 保持鼓励性质

语气要求：
- 友好亲切
- 充满趣味
- 避免说教
- 适当使用表情符号
- 可以适度调侃


# 导入数据规范化格式
## 基本结构
```json
{
  "records": [
    {
      "date": "YYYY-MM-DD",  // 日期格式
      "meals": [
        {
          "time": "HH:mm",   // 24小时制时间
          "type": "餐次类型", // 固定枚举值
          "foods": [
            {
              "name": "食物名称",  // 使用标准名称
              "amount": "份量",    // 标准计量单位
              "category": "类别",  // 固定分类
              "calories": 数值     // 精确到小数点后1位
            }
          ]
        }
      ]
    }
  ]
}
```

## 规范细则

### 1. 日期和时间格式
- 日期：必须使用 `YYYY-MM-DD` 格式
- 时间：必须使用24小时制 `HH:mm` 格式

### 2. 餐次类型（type）固定枚举值
```js
const MEAL_TYPES = {
  breakfast: "早餐",
  lunch: "午餐",
  dinner: "晚餐",
  snack: "加餐"
}
```

### 3. 食物分类（category）标准
```js
const FOOD_CATEGORIES = {
  "主食": ["米饭", "面包", "面条", "馒头"],
  "蛋白质": ["蛋类", "禽类", "水产", "豆制品"],
  "蔬菜": ["叶菜类", "根茎类"],
  "水果": ["新鲜水果"],
  "乳制品": ["牛奶", "酸奶", "奶酪"],
  "零食": ["点心", "糖果", "饼干"],
  "饮品": ["茶", "咖啡", "果汁"],
  "油脂": ["油", "坚果", "黄油"]
}
```

### 4. 标准计量单位
```js
const UNITS = {
  重量: ["g", "克", "kg"],
  体积: ["ml", "毫升", "L"],
  个数: ["个", "只", "枚"],
  份量: ["份", "盘", "碗", "杯"],
  其他: ["根", "串", "片", "块"]
}
```

## 示例数据
```json
{
  "records": [
    {
      "date": "2024-02-01",
      "meals": [
        {
          "time": "08:00",
          "type": "breakfast",
          "foods": [
            {
              "name": "牛奶",
              "amount": "250ml",
              "category": "乳制品",
              "calories": 150.0
            }
          ]
        }
      ]
    }
  ]
}
```

## 数据验证规则
1. 日期必须有效且不能是未来日期
2. 时间必须在00:00-23:59范围内
3. 餐次类型必须是预定义的枚举值
4. 食物类别必须符合标准分类
5. 卡路里值必须大于0且保留一位小数
6. 所有必填字段不能为空

## 错误示例
```json
{
  "records": [
    {
      "date": "2024/02/01",      // 错误：日期格式不正确
      "meals": [
        {
          "time": "8:00",        // 错误：时间格式不规范
          "type": "morning",     // 错误：非标准餐次类型
          "foods": [
            {
              "name": "牛奶",
              "amount": "一杯",   // 错误：使用非标准计量单位
              "category": "饮料", // 错误：非标准分类
              "calories": "150"   // 错误：应为数值类型
            }
          ]
        }
      ]
    }
  ]
}
```

# 测试用例
{
  "records": [
    {
      "date": "2023-12-26",
      "meals": [
        {
          "time": "08:00",
          "type": "breakfast",
          "foods": [
            {
              "name": "茶叶蛋",
              "amount": "1个",
              "category": "蛋类",
              "calories": 77.5
            },
            {
              "name": "水煮蛋",
              "amount": "1个",
              "category": "蛋类",
              "calories": 77.5
            }
          ]
        },
        {
          "time": "12:00",
          "type": "lunch",
          "foods": [
            {
              "name": "玉米",
              "amount": "1根",
              "category": "主食",
              "calories": 232
            },
            {
              "name": "红薯",
              "amount": "1个",
              "category": "根茎类",
              "calories": 76
            }
          ]
        },
        {
          "time": "18:00",
          "type": "dinner",
          "foods": [
            {
              "name": "苹果",
              "amount": "1个",
              "category": "水果",
              "calories": 78
            },
            {
              "name": "酸奶",
              "amount": "1盒",
              "category": "乳制品",
              "calories": 140
            }
          ]
        }
      ]
    },
    {
      "date": "2023-12-27",
      "meals": [
        {
          "time": "08:00",
          "type": "breakfast",
          "foods": [
            {
              "name": "水煮鸡蛋",
              "amount": "1个",
              "category": "蛋类",
              "calories": 77.5
            },
            {
              "name": "茶叶蛋",
              "amount": "1个",
              "category": "蛋类",
              "calories": 77.5
            }
          ]
        },
        {
          "time": "12:00",
          "type": "lunch",
          "foods": [
            {
              "name": "鸡肉沙拉",
              "amount": "一份",
              "category": "混合",
              "calories": 280
            }
          ]
        },
        {
          "time": "15:30",
          "type": "snack",
          "foods": [
            {
              "name": "草莓糖葫芦",
              "amount": "一串",
              "category": "零食",
              "calories": 120
            }
          ]
        },
        {
          "time": "18:00",
          "type": "dinner",
          "foods": [
            {
              "name": "希腊酸奶",
              "amount": "一盒",
              "category": "乳制品",
              "calories": 63
            }
          ]
        }
      ]
    },
    {
      "date": "2023-12-28",
      "meals": [
        {
          "time": "12:00",
          "type": "lunch",
          "foods": [
            {
              "name": "番茄汁",
              "amount": "一杯",
              "category": "饮品",
              "calories": 50
            },
            {
              "name": "生菜沙拉",
              "amount": "一份",
              "category": "蔬菜",
              "calories": 30
            },
            {
              "name": "鸡腿肉",
              "amount": "1个",
              "category": "禽类",
              "calories": 200
            },
            {
              "name": "意面",
              "amount": "半份",
              "category": "主食",
              "calories": 110
            }
          ]
        },
        {
          "time": "15:30",
          "type": "snack",
          "foods": [
            {
              "name": "烤鸡胸肉",
              "amount": "半份",
              "category": "禽类",
              "calories": 82.5
            }
          ]
        },
        {
          "time": "18:00",
          "type": "dinner",
          "foods": [
            {
              "name": "希腊酸奶",
              "amount": "一盒",
              "category": "乳制品",
              "calories": 105
            },
            {
              "name": "苹果",
              "amount": "1个",
              "category": "水果",
              "calories": 78
            }
          ]
        }
      ]
    },
    {
      "date": "2023-12-29",
      "meals": [
        {
          "time": "12:00",
          "type": "lunch",
          "foods": [
            {
              "name": "烤鸡胸肉",
              "amount": "半份",
              "category": "禽类",
              "calories": 82.5
            },
            {
              "name": "生菜沙拉",
              "amount": "一份",
              "category": "蔬菜",
              "calories": 30
            },
            {
              "name": "紫薯",
              "amount": "1个",
              "category": "根茎类",
              "calories": 76
            },
            {
              "name": "鸡腿肉",
              "amount": "1个",
              "category": "禽类",
              "calories": 200
            }
          ]
        },
        {
          "time": "18:00",
          "type": "dinner",
          "foods": [
            {
              "name": "沙拉",
              "amount": "1份",
              "category": "蔬菜",
              "calories": 30
            },
            {
              "name": "苹果",
              "amount": "1个",
              "category": "水果",
              "calories": 78
            },
            {
              "name": "酸奶",
              "amount": "1杯",
              "category": "乳制品",
              "calories": 175
            }
          ]
        }
      ]
    },
    {
      "date": "2023-12-30",
      "meals": [
        {
          "time": "08:00",
          "type": "breakfast",
          "foods": [
            {
              "name": "茶叶蛋",
              "amount": "1个",
              "category": "蛋类",
              "calories": 77.5
            },
            {
              "name": "香菇菜包",
              "amount": "1个",
              "category": "主食",
              "calories": 180
            }
          ]
        },
        {
          "time": "12:00",
          "type": "lunch",
          "foods": [
            {
              "name": "水煮虾",
              "amount": "1小盘",
              "category": "水产",
              "calories": 85
            },
            {
              "name": "炒上海青",
              "amount": "1小盘",
              "category": "叶菜类",
              "calories": 20
            },
            {
              "name": "炒胡萝卜",
              "amount": "半份",
              "category": "根茎类",
              "calories": 20.5
            },
            {
              "name": "糯玉米",
              "amount": "半根",
              "category": "主食",
              "calories": 116
            }
          ]
        },
        {
          "time": "18:00",
          "type": "dinner",
          "foods": [
            {
              "name": "生菜沙拉",
              "amount": "1份",
              "category": "蔬菜",
              "calories": 30
            },
            {
              "name": "苹果",
              "amount": "1个",
              "category": "水果",
              "calories": 78
            }
          ]
        }
      ]
    },
    {
      "date": "2023-12-31",
      "meals": [
        {
          "time": "08:00",
          "type": "breakfast",
          "foods": [
            {
              "name": "茶叶蛋",
              "amount": "1个",
              "category": "蛋类",
              "calories": 77.5
            },
            {
              "name": "香菇菜包",
              "amount": "1个",
              "category": "主食",
              "calories": 180
            }
          ]
        },
        {
          "time": "12:00",
          "type": "lunch",
          "foods": [
            {
              "name": "水煮虾",
              "amount": "1小盘",
              "category": "水产",
              "calories": 85
            },
            {
              "name": "炒上海青",
              "amount": "1小盘",
              "category": "叶菜类",
              "calories": 20
            },
            {
              "name": "炒胡萝卜",
              "amount": "半份",
              "category": "根茎类",
              "calories": 20.5
            },
            {
              "name": "糯玉米",
              "amount": "半根",
              "category": "主食",
              "calories": 116
            }
          ]
        },
        {
          "time": "18:00",
          "type": "dinner",
          "foods": [
            {
              "name": "生菜沙拉",
              "amount": "1份",
              "category": "蔬菜",
              "calories": 30
            },
            {
              "name": "苹果",
              "amount": "1个",
              "category": "水果",
              "calories": 78
            }
          ]
        }
      ]
    }
  ]
}
