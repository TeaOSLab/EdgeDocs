# 访问日志相关服务

## 列出单页访问日志 - /HTTPAccessLogService/ListHTTPAccessLogs
### 请求参数
~~~protobuf
{
	string requestId = 1; // 上一页请求ID，可选
	int64 serverId = 2; // 服务ID
	int64 size = 3; // 单页条数
	string day = 4; // 日期，格式YYYYMMDD
	bool reverse = 5; // 是否反向查找，可选
	bool hasError = 6; // 是否有错误，可选
	int64 firewallPolicyId = 7; // WAF策略ID，可选
	int64 firewallRuleGroupId = 8; // WAF分组ID，可选
	int64 firewallRuleSetId = 9; // WAF规则集ID，可选
}
~~~

