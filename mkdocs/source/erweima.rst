第九章 二维码
==============================

9.1 X93新增
---------------------

按交易码查询::

  SELECT  * FROM bcss01.BCSS_JOURNAL_TRAN 
  WHERE TRAN_DATE='20190307' AND 
  TRAN_CODE IN ('A01312','A10312','A10236','A10313');
  
主扫查询订单(它代本)（A01312）验证::

  select dump(RECV_PKG,16),REPLY_PKG from bcss01.BCSS_JOURNAL_TRAN where 
  TRAN_DATE='20190307' AND TRAN_CODE='A01312';
  
主扫查询订单（A10312）验证::
 
  select RECV_PKG, dump(REPLY_PKG,16) from bcss01.BCSS_JOURNAL_TRAN 
  where TRAN_DATE='20190307' AND TRAN_CODE='A10312';
  
C2B消费结果通知（A10236）验证::

  select dump(ACCEPT_PKG,16),SEND_PKG from bcss01.BCSS_JOURNAL_TRAN 
  where TRAN_DATE='20190307' AND TRAN_CODE='A10236';
  
主扫付款(A10313)验证::

  select dump(ACCEPT_PKG,16),SEND_PKG from bcss01.BCSS_JOURNAL_TRAN 
  where TRAN_DATE='20190307' AND TRAN_CODE='A10313';
  
  