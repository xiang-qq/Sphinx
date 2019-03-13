第九章 常用查询语句
==============================

9.1 查询微信交易
---------------------

常用查询语句::

  select appid,mch_id,SUB_APPID,SUB_MCH_ID,
  OUT_TRADE_NO,TOTAL_FEE,RETURN_CODE ,
  RETURN_MSG,RESULT_CODE,ERR_CODE,ERR_CODE_DES,
  TRADE_STATE,OUT_REFUND_NO 
  from bcss_journal_wechat 
  where tran_date='20171124' 
  and tran_code=’A43051’;
  
说明：RETURN_CODE取值为SUCCESS/FAIL,代表通讯返回码，RETURN_MSG代表通讯错误返回信息
RETURN_CODE为成功时，才会有RESULT_CODE,ERR_CODE, ERR_CODE_DES字段，
其中RESULT_CODE为SUCCESS时，ERR_CODE, ERR_CODE_DES无值，为FAIL时有值，代表业务失败
TRADE_STATE代表具体的业务处理结果，参见数据字典。


9.2 查询支付宝交易
---------------------

常用查询语句::

  select app_id, out_trade_no,trade_no,
  refund_amount,gateway_code,gateway_msg,
  sub_code,sub_msg 
  from bcss_journal_alipay 
  where tran_date='20171124' 
  and tran_code=’A50801’;

说明：code为10000,代表交易成功，sub_code,sub_msg都为空
code不为10000时，代表交易失败，具体的交易错误码和信息，参考sub_code,sub_msg值。


9.3 统一APP开户及结果查询                             
--------------------------                  
                                       
常用查询语句::

  select query_id,recv_pkg 
  from bcss_journal_app 
  where tran_date=’20171218’ 
  and tran_code=’A9X701’


9.4 统一APP查询账单查询                                      
------------------------                           
 
常用查询语句::
                                               
  select f2,f48,f39,ap_ret_code,ap_ret_msg 
  from bcss_journal_sw 
  where tran_date=’20171218’ 
  and tran_code=’C66X01’

