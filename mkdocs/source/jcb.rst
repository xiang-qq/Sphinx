第一章 JCB
======================

1.1 我行ATM发起的交易
---------------------

重点交易码：余额查询-C11303、取现- C11302、取现冲正-C11703
交易路劲：ATM->ATMP->IPS->BCSS->JCB
查询语句::

	select F2,F39,tran_state,rever_state 
	from bcss01.bcss_journal_sw 
	where tran_code='C11303' and 
	tran_date='20180805';

F39为00代表交易成功，冲正中rever_state为0代表原交易成功并已冲正


1.2 我行POS发起的交易
---------------------

重点交易码：消费-C11102、预授权-C11101、消费冲正-C11701
交易路劲：POS->POSP->IPS->BCSS->JCB
查询语句::

	select F2,F39,tran_state,rever_state 
	from bcss01.bcss_journal_sw 
	where tran_code='C11102' and 
	tran_date='20180805';
	
F39为00代表交易成功，冲正中rever_state为0代表原交易成功并已冲正


1.3	JCB发起的我行EISS交易
-----------------------------------

重点交易码：余额查询C23103、消费-C23101、消费冲正-C23701、取现-C23102、取现冲正C23703
交易路劲：JCB->BCSS->IPS->EISS
查询语句::

	select F2,F39,tran_state,rever_state 
	from bcss_journal_sw 
	where tran_code='C23103' and 
	tran_date='20180805';



