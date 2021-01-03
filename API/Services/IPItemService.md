# IP条目相关服务

## 创建IP - /IPItemService/CreateIPItem
### 请求参数
~~~
{
	int64 ipListId = 1; // IP列表ID
	string ipFrom = 2; // 开始IP
	string ipTo = 3; // 结束IP（可选）
	int64 expiredAt = 4; // 过期时间戳（可选）
	string reason = 5; // 加入理由（可选）
}
~~~

## 修改IP - /IPItemService/UpdateIPItem
### 请求参数
~~~
{
	int64 ipItemId = 1;
	string ipFrom = 2;
	string ipTo = 3;
	int64 expiredAt = 4;
	string reason = 5;
}
~~~

## 删除IP - /IPItemService/DeleteIPItem
### 请求参数
~~~
{
	int64 ipItemId = 1;
}
~~~

## 计算IP数量 - /IPItemService/CountIPItemsWithListId
### 请求参数
~~~
{
	int64 ipListId = 1;
}
~~~

## 列出单页的IP - /IPItemService/ListIPItemsWithListId
### 请求参数
~~~
{
	int64 ipListId = 1;
	int64 offset = 2;
	int64 size = 3;
}
~~~