
第七章 301医院项目
====================== 

7.1 概述               
--------------------------

301医院项目主要用于北京分行和301医院合作，
使用301医院APP进行挂号、缴费（微信、支付宝）。

7.2 微信新增交易码与路径
--------------------------

微信预下单-A33501、微信关闭订单-A33502、微信查询订单-A33503、微信申请退款-A33504
交易路径：BIBP->BCSS->微信,直连模式，X810后变为间连，交易码也会改变     
		  
7.3 微信新增交易查询语句
--------------------------

1、	查询北分发起的交易（下单、查询、关闭）是否成功::

  select tran_date,tran_time,tran_state,ap_ret_code,
  ap_ret_msg,return_code,result_code,err_code 
  from bcss_journal_wechat 
  where tran_date='20180910' 
  and tran_code='A33501' 
  and out_trade_no='123456666';             

根据商户订单号查询，AP_RET_CODE为’0000000’代表BCSS处理成功，如想看业务是否成功，
则看return_code和result_code两个字段值都应为’SUCCESS；

2、	查询北分发起的退货交易是否成功::

  select tran_date,tran_time,tran_state,ap_ret_code,
  ap_ret_msg,return_code,result_code,err_code 
  from bcss_journal_wechat where tran_date='20180910' 
  and tran_code='A33504' 
  and out_refund_no='123456666';

根据商户退款单号查询，AP_RET_CODE为’0000000’代表BCSS处理成功，如想看业务是否成功，
则看return_code和result_code两个字段值都应为’SUCCESS’;

3、	按照错误码统计微信交易信息::
  
  select tran_code,ap_ret_code,count(*) 
  from bcss_journal_wechat 
  where tran_date='20180910' 
  and tran_code in('A33501','A33502','A33503','a33504') 
  group by tran_code,ap_ret_code;
  
7.4 支付宝新增交易码与路径
----------------------------

支付宝查询订单-A34601、支付宝撤销交易-A34602、支付宝退款交易-A34603
交易路径：BIBP->BCSS->支付宝,直连模式

7.5 支付宝新增交易查询语句
----------------------------

1、	查询北分发起的交易是否成功::

  select tran_date,tran_time,tran_state,ap_ret_code,
  gateway_code,gateway_msg,sub_code,sub_msg 
  from bcss_journal_alipay 
  where tran_date='20180910' 
  and  tran_code='A34601' 
  and out_trade_no='122333';             

根据商户退款单号查询，AP_RET_CODE为’0000000’代表BCSS处理成功，如想看业务是否成功，
则看gateway_code应为10000，其他错误再看sub_code和sub_msg

2、	按照错误码统计支付宝交易信息::

  select tran_code,ap_ret_code,count(*) 
  from bcss_journal_alipay 
  where tran_date='20180910' 
  and tran_code 
  in ('A34601','A34602','A34603') 
  group by tran_code,ap_ret_code;

可以将ap_ret_code换成gateway_code查询业务成功情况。

 