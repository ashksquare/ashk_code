create or replace table app_payments.app_payments_analyticstemp.temp_leading_indicator_activated_2019 as 

with activated_2019 as (
select user_token as merchant_token
    , first_successful_activation_request_created_at as act_at
    , npa_total / 100 as npa_usd
    , business_category
from app_bi.pentagon.dim_user 
where user_type = 'MERCHANT'
    and country_code = 'US'
    and year(first_successful_activation_request_created_at) = 2019
)

select a.*
    , min(fpt.payment_trx_recognized_at) as first_pmt_at
    , min(case when fpt.amount_base_unit > 100 then fpt.payment_trx_recognized_at else null end) as first_non_test_pmt_at
    
    , count(case when datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 7 then payment_token else null end) as pmt_7d
    , count(case when datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 14 then payment_token else null end) as pmt_14d
    , count(case when datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 21 then payment_token else null end) as pmt_21d
    , count(case when datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 28 then payment_token else null end) as pmt_28d
    , count(case when datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 35 then payment_token else null end) as pmt_35d
    
    -- , sum(case when datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 7 then ceil(amount_base_unit / 10000) else 0 end) as amount_7d
    -- , sum(case when datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 14 then ceil(amount_base_unit / 10000) else 0 end) as amount_14d
    -- , sum(case when datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 21 then ceil(amount_base_unit / 10000) else 0 end) as amount_21d
    -- , sum(case when datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 28 then ceil(amount_base_unit / 10000) else 0 end) as amount_28d
    -- , sum(case when datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 35 then ceil(amount_base_unit / 10000) else 0 end) as amount_35d
    
    , count(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 7 then payment_token else null end) as non_test_pmt_7d
    , count(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 14 then payment_token else null end) as non_test_pmt_14d
    , count(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 21 then payment_token else null end) as non_test_pmt_21d
    , count(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 28 then payment_token else null end) as non_test_pmt_28d
    , count(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 35 then payment_token else null end) as non_test_pmt_35d
    
    , count(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 7 and product_name = 'Register POS' then payment_token else null end) as non_test_pos_pmt_7d
    , count(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 14 and product_name = 'Register POS' then payment_token else null end) as non_test_pos_pmt_14d
    , count(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 21 and product_name = 'Register POS' then payment_token else null end) as non_test_pos_pmt_21d
    , count(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 28 and product_name = 'Register POS' then payment_token else null end) as non_test_pos_pmt_28d
    , count(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 35 and product_name = 'Register POS' then payment_token else null end) as non_test_pos_pmt_35d    
    
    -- , sum(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 7 then ceil(amount_base_unit / 10000) else 0 end) as non_test_amount_7d
    -- , sum(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 14 then ceil(amount_base_unit / 10000) else 0 end) as non_test_amount_14d
    -- , sum(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 21 then ceil(amount_base_unit / 10000) else 0 end) as non_test_amount_21d
    -- , sum(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 28 then ceil(amount_base_unit / 10000) else 0 end) as non_test_amount_28d
    -- , sum(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 35 then ceil(amount_base_unit / 10000) else 0 end) as non_test_amount_35d
    
    --, sum(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 365 and product_name = 'Register Terminal' then ceil(amount_base_unit / 10000) else 0 end) as term_nva
    --, sum(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 365 and product_name = 'Register POS' then ceil(amount_base_unit / 10000) else 0 end) as spos_nva
    --, sum(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 365 and product_name = 'Virtual Terminal' then ceil(amount_base_unit / 10000) else 0 end) as vt_nva
    --, sum(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 365 and product_name = 'Invoices' then ceil(amount_base_unit / 10000) else 0 end) as inv_nva
    --, sum(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 365 and product_name = 'eCommerce API' then ceil(amount_base_unit / 10000) else 0 end) as ecom_nva
    --, sum(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 365 and is_card_present = 1 then ceil(amount_base_unit / 10000) else 0 end) as cp_nva
    --, sum(case when fpt.amount_base_unit > 100 and datediff('day',a.act_at,fpt.payment_trx_recognized_at) < 365 and is_card_present = 0 then ceil(amount_base_unit / 10000) else 0 end) as cnp_nva
    
    from app_bi.pentagon.fact_payment_transactions fpt
    left join app_bi.pentagon.dim_user du on fpt.unit_token = du.user_token and du.user_type = 'UNIT'
    inner join activated_2019 a on a.merchant_token = du.best_available_merchant_token
    where is_gpv = 1
    group by 1,2,3,4
