Sequelize

sequelize是 mysql的orm框架

## 模型

模型通过init方法建立和表之间的映射， 每列必须具有数据类型

```javascript
class Project extends Model {
  get fullname(){
    return this.getDataValue('title') + '|||'
  }
  set fullname(value){
    return this.setDataValue('title', value.splice(0, 10))
  }
}
Project.init({
	title: {
    type: Sequelize.BOOLEAN, // 类型
    defaultValue: true, // 默认值
    allowNull: false, // 是否允许是null
    unique: true, // 用来创建一个唯一约束
    primaryKey: true, // 定义主键
    autoIncrement: true, // 创建自增的整数列
		//创建一个外键
    bar_id: {
      type: Sequelize.INTEGER,
      references: {
        model: bar, //引用另一个模型
        key: 'id', // 引用模型的列名称
      }
    },
    validate: { // 验证
      is: /^[a-z]+$/i //只允许字母,
      not: ["[a-z]", 'i'] //不允许字母
    	isEmail: true,
    	isUrl: true,
    	isIP: true,
    	isIPv4: true,
    	isIPv6: true,
    	isAlpha: true,            // 只允许字母
      isAlphanumeric: true,     // 只允许使用字母数字
      isNumeric: true,          // 只允许数字
      isInt: true,              // 检查是否为有效整数
      isFloat: true,            // 检查是否为有效浮点数
      isDecimal: true,          // 检查是否为任意数字
      isLowercase: true,        // 检查是否为小写
      isUppercase: true,        // 检查是否为大写
      notNull: true,            // 不允许为空
      isNull: true,             // 只允许为空
	    notEmpty: true,           // 不允许空字符串
      equals: 'specific value', // 只允许一个特定值
      contains: 'foo',          // 检查是否包含特定的子字符串
      notIn: [['foo', 'bar']],  // 检查是否值不是其中之一
      isIn: [['foo', 'bar']],   // 检查是否值是其中之一
      notContains: 'bar',       // 不允许包含特定的子字符串
      len: [2,10],              // 只允许长度在2到10之间的值
      isUUID: 4,                // 只允许uuids
      isDate: true,             // 只允许日期字符串
      isAfter: "2011-11-05",    // 只允许在特定日期之后的日期字符串
      isBefore: "2011-11-05",   // 只允许在特定日期之前的日期字符串
      max: 23,                  // 只允许值 <= 23
      min: 23,                  // 只允许值 >= 23
      isCreditCard: true,       // 检查有效的信用卡号码
        // 自定义验证器的示例:
      isEven(value) {
        if (parseInt(value) % 2 !== 0) {
          throw new Error('Only even values are allowed!');
        }
      }
      isGreaterThanOtherField(value) {
        if (parseInt(value) <= parseInt(this.otherField)) {
          throw new Error('Bar must be greater than otherField.');
        }
      }
    }
  }
}, {})
```

定义好模型之后，需要通过`sync`方法在数据库中建立表



## 数据类型



## 查询

### find 查询数据库中一个特定的元素

```javascript
Project.findByPk(123).then(project => {
  // project 将是Project的一个实例, 并具有在表中存在id为123条目的内容
  // 如果没有获得null
})

Project.findOne({where:  {title: 'aProject'}}).then(project => {
  // project将是Project表中title为`aProject`的第一个条目 || null
})

Project.findOne({
  where: {title: 'aProject'},
  attributes: ['id', ['name', 'title']] // attributes 只想要某些属性
}).then(project => {
  // project将是Projects表中title为`aProject`的第一个条目 || null
  //  project.get('title') 将包含project的name
})
```



### findOrCreate 搜索特定的元素或创建它

检查数据库是否已存在某个元素, 如果是这种情况, 则该方法将生成相应的实例, 如果不存在, 将会被创建.	

```javascript
User.findOrCreate({
	where: { username: 'sdepold'}, 
	defaults: {job: 'technical lead javascript'}
})
.then(([user, created]) => {
	// 如果是新建的, created为true，否则为false
})
```

### findAndCountAll 在数据库中搜索多个元素, 返回一个对象包含数据(rows)和总计数(count)

```javascript
Project.findAndCountAll({
  where: {
    title: {
      [Op.like]: 'foo%'
    }
  },
  include: [ //支持include, 只有标记为required的include将被添加到计数部分
    {model: Profile, required: true},
    {model: User, where: {active: true}} // 在include中添加一个where语句使它自动成为required
  ]
  offset: 10,
  limit: 2
})
.then(result => {
  console.log(result.count)
  console.log(result.rows)
}) 
```

### findAll 搜索数据库中的多个元素

```javascript
// 找到多个条目
Project.findAll().then(projects => {
  // projects 将是所有Project实例的数组
})
// 搜索特定属性 使用哈希
Project.findAll({
  where: { name: 'a project'}
})
.then(projects => {
  // projects 将是一个具有指定name的Project实例数组
})

// 在特定范围内进行搜索
Project.findAll({
  where: {
    id: [1,2,3]
  }
})
.then(projects => {
  // projects将是一系列具有id 1or2or3的项目
})

Project.findAll({
  where: {
    id: {
      [Op.and]: {a: 5}, //且a为5
      [Op.or]: [{a: 5}, {a:6}], // a=5或a=6
      [Op.gt]: 6, // id > 6
      [Op.gte]: 6, //id >= 6
      [Op.lt]: 10, // id < 10
      [Op.lte]: 10, // id <= 10
      [Op.ne]: 20, //id != 20
      [Op.between]: [6,10], // id在 6和10之间
      [Op.notBetween]: [11,15] // id不在 11和15 之间
      [Op.in]: [1,2] // id在1，2之中
    	[Op.notIn]: [1,2] // 不在 1，2之中
      [Op.like]: '%hat', //包含%hat
  		[Op.notLike]: '%hat', //不包含%hat
    },
     status: {
       [Op.not]: false // status 不为false
     }
  }
})
```



### 原始查询

有时候,你可能会期待一个你想要显示的大量数据集,而无需操作. 

```javascript
Project.findAll({where: {}, raw: true})

```

### 计数 count方法

```javascript
Project.count().then( c => {}) // c是出现
```

### 最大值 max

获取属性的最大值

```javascript
// 3条数据 10 20 40
Project.max('age').then(max => {
 // 返回40
})
```

### 最小值 min

获取属性的最小值

```javascript
Project.min('age').then(min => {})
```

### 特定属性求和 sum

为了计算表的特定列的总和, 可以使用sum方法

```javascript
Project.sum('age').then(sum => {})
```



## 增

### build 

返回一个未保存的对象, 需要明确的保存

```javascript
const project = Project.build({
	title: 'my awesome project'，
	description: 'woot woot'
})
```



### save

将未保存的对象存储到数据库中

```javascript
project.save({fields: []}).then()
```

*fields将定义哪些字端被修改*

### create

直接保存到数据库中

#### 批量创建

```
Project.bulkCreate({
	a: {},
	b: {},
	c: {}
}, {fields: [], validate: true}) //第二个参数为一个对象， 
```

## 删

### destroy

```
project.destroy()
```

*paranoid* 为true将进行软删除, 把deleteAt设置为当前时间戳, 对象被软删除之后, 如果没有强制删除, 将无法使用相同的主键

*restore* 通过restore方法可以恢复软删除的数据

*force: true* 强制删除

#### 批量删除

```
Project.destroy({
	where: {} //批量删除哪些
})
```



## 改

update

```
project.update({title: 'new value'}, {fields: []}).then()
```

*fields将定义哪些字端被修改*

#### 批量更新

```
Project.update(
{ status: 'inactive'}，// 批量修改的字段
{ where: {}} // where规则
)
```



### increment 某个属性递增

```
User.findByPk(1).then(user => {
	return user.increment(key or keyArr, {by: 2}) //key 哪个属性, by 从几开始
})

// 对象形式
User.findByPk(1).then(user => {
	return user.increment({
		key: 3,
		key2: 4
	})
})
```

### decrement  某个属性递减

```
User.findByPk(1).then(user => {
	return user.decrement(key or keyArr, {by: 22})
})
// 对象形式
User.findByPk(1).then(user => {
	return user.decrement({
		key: 3,
		key2: 10
	})
})
```

## 关联

### 来源 Source

### 目标 Target

### 一对一关联 hasOne

```javascript
class User extends Model{}
User.init({
  name: Sequelize.STRING，
  email: Sequelize.STRING
}, {
  sequelize,
  modelName: 'user'
})

class Project extends Model{}
Project.init({
  name: Sequelize.STRING
}, {
  sequelize,
  modelName: 'project'
})

User.hasOne(Project)
// User 模型(调用函数的模型)是 来源(Source). Project 模型(作为参数传递的模型)是 目标(Target).
```

### 外键

当你在模型中创建关联时, 会自动创建带约束的外键引用

```javascript
class Task extends Model{}
Task.init({title: Sequelize.STRING}, {sequelize, modelName: 'task'})
class User extends Model{}
Model.init({userName: Sequelize.STRING}, {sequelize, modelName: 'user'})

User.hasMany(Task) // 将userId添加到Task模型
Task.belongsTo(user) // 同样会将userId添加到Task模型中
```



