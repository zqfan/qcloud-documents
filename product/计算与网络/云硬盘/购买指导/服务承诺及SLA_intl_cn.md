#CBS云硬盘等级协议(SLA)

##1 腾讯云服务
腾讯云服务：指为满足各类网站、应用等各种产品的不同需求，由腾讯云提供的云服务器、云带宽、云存储空间、云数据库、云安全、云监控、云拨测等各种不同要素组合成的云系统服务。具体服务类别以腾讯云公开发布的相关服务信息为准。
##2 服务保证指标
腾讯云为您所购买的云服务制定服务等级指标，并向您承诺提供数据管理和业务质量方面最大程度的保障。同时，腾讯云有权根据变化适时对部分指标作出调整。若无特殊约定，本条款中的“月”均指30个自然日，按自然月计算。
2.1 CBS云硬盘服务
2.1.1 数据存储的持久性
每月您申请的CBS云硬盘的持久性99.999999%。
2.1.2 数据可销毁性
在您要求删除数据或设备在弃置、转售前，腾讯云将采取磁盘低级格式化操作彻底删除您所有数据，并无法复原，硬盘到期报废时将进行消磁。
2.1.3 数据私密性
CBS云硬盘可结合kms加密服务，在消息生产时，将消息body加密，避免明文上传。
2.1.4 数据知情权
目前用户CBS云硬盘服务部署在六大数据中心，分别是：上海数据中心、广州数据中心、北京数据中心、香港数据中心、新加坡数据中心、北美数据中心。
帮助用户选择网络条件最好的数据中心存储数据，用户购买云服务器时刻选择归属的地域（广州、上海、北京、香港、新加坡、北美）。
用户已知的数据中心均遵守的当地的法律和中华人民共和国相关法律。
用户所有数据不会提供给任意第三方，除政府监管部门监管审计需要。用户所有数据不会存在国外数据中心或用于国外业务或数据分析。
为保证用户数据安全性，腾讯云采用同时存储三份数据副本的存储方式，并定期进行数据冷备操作。2.1.5 数据可审查性
腾讯云在依据现有法律法规体系下，出于配合政府监管部门的监管或安全取证调查等原因的需要，在符合流程和手续完备的情况下，可以提供云服务器相关信息，包括关键组件的运行日志、运维人员的操作记录、用户操作记录等信息。
2.1.6 业务可用性
CBS云硬盘承诺99.95%的业务可用性，即用户每月可用时间应为30天24小时60分钟*99.95%=43178.4 分钟，即存在43200-43178.4=21.6分钟的不可用时间，其中业务不可用的统计单元为用户单业务实例。
业务故障的恢复正常时间5分钟以下，不计入业务不可用性计算中，不可用时间指业务发生故障开始到恢复正常使用的时间，包括维护时间。超过5分钟的，纳入不可用时间。
2.1.7故障恢复能力
CBS云硬盘具备故障迁移能力，可在物理服务器故障发生时，无需用户参与，自动将业务迁移至新的母机，保证客户服务的连续性。同时，腾讯云提供专业团队7x24小时帮助维护。
##3 服务计量准确性
腾讯云服务的费用在用户的选购页面和订单页面均有明确展示，用户可自行选择具体服务类型并按列明的价格进行购买。具体价格以腾讯云官网公布的价格为准，腾讯云按照用户选购的云服务规格和使用时长进行收费。

##4 补偿
4.1 适用范围适用于由腾讯云故障原因导致用户的云服务器不可正常使用或完全不可访问，以及腾讯云故障导致的网站（开发者服务网站）无法访问时，用户要求腾讯云针对事故/故障而进行的补偿。4.2 补偿标准原则故障时间=故障解决时间-故障开始时间。按分钟计算故障时间，故障时间小于1分钟的按1分钟计算。例如，故障时间为1分01秒，按2分钟算。CBS云硬盘故障百倍赔偿：（1）后付费：赔偿方式是补偿现金券，现金券金额=故障Queue每天费用/24/60×故障时间×100。赔偿现金券的上限，不超过CBS云硬盘的服务总费用。