
第五章 北师大跨屏支付
====================== 

5.1 本次新增交易               
--------------------------

支付宝下单：A54605  支付宝查询：A54606        
微信下单：A53505    微信查询：A53506        
本次修改交易流程：A76504/A76506 间连微信公众号通知交易

5.2 支付宝新增交易
--------------------------

	select t.tran_code,t.ap_ret_code,t.tran_state,count(1)   
	from bcss_journal_alipay t where --t.tran_date='20180619'
	t.tran_code in ('A54605','A54606')                       
	group by t.tran_code,t.ap_ret_code,t.tran_state;         
		  
5.3 微信新增交易
---------------------

  select t.tran_code,t.ap_ret_code,t.tran_state,count(1)       
  from bcss_journal_wechat t where --t.tran_date='20180619' and
  t.tran_code in ('A53505','A53506')                           
  group by t.tran_code,t.ap_ret_code,t.tran_state;             

5.4 间连微信公众号通知交易                                                        
----------------------------                                             
                                                                  
  select t.tran_code,t.ap_ret_code,t.tran_state,count(1)         
  from bcss_journal_wechat t where --t.tran_date='20180619' and  
  t.tran_code in ('A76504','A76506')                             
  group by t.tran_code,t.ap_ret_code,t.tran_state;    
  
5.5 轮询交易是否触发                                                     
---------------------                                                                                                    
                                                       
  select t.notify_flag, t.total_times, t.remain_times          
  from bcss_journal_alipay t where --t.tran_date='20180619' and
  t.tran_code = 'A54605';                                      
  select t.notify_flag, t.total_times, t.remain_times          
  from bcss_journal_wechat t where --t.tran_date='20180619' and
  t.tran_code = 'A53505';                                      
                                                             
  select t.tran_code,t.ap_ret_code,t.tran_state,count(1)       
  from bcss_journal_alipay t where --t.tran_date='20180619' and
  t.tran_code='A6X601'                                         
  group by t.tran_code,t.ap_ret_code,t.tran_state;             
  select t.tran_code,t.ap_ret_code,t.tran_state,count(1)       
  from bcss_journal_wechat t where --t.tran_date='20180619' and
  t.tran_code='A6X503'                                         
  group by t.tran_code,t.ap_ret_code,t.tran_state;         
  
5.6 本次新增交易，关联到轮询交易                                              
----------------------------------                               
                                                    
  select t2.tran_code,t2.ap_ret_code,t2.tran_state,count(1)  
  from bcss_journal_alipay t1, bcss_journal_alipay t2        
  where t1.tran_code='A54605' and t2.tran_code='A6X601'      
  and t1.tran_date = t2.tran_date                            
  and t1.out_trade_no = t2.out_trade_no                      
  group by t2.tran_code,t2.ap_ret_code,t2.tran_state;        
                                                             
  select t2.tran_code,t2.ap_ret_code,t2.tran_state,count(1)  
  from bcss_journal_wechat t1, bcss_journal_wechat t2        
  where t1.tran_code='A53505' and t2.tran_code='A6X503'      
  and t1.tran_date = t2.tran_date                            
  and t1.out_trade_no = t2.out_trade_no                      
  group by t2.tran_code,t2.ap_ret_code,t2.tran_state;        
  
  