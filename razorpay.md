#                 Razorpay

nodejs

-> npm install razorpay

-> generate order id

const razorpay=new Razorpay({
    key_id:"",
    key_secret:""
})

coonst options={
    amount:100,
    currency:"INR",
    receipt:"receipt#1"
    payment_capture:1
}

const response=await razorpay.order.create(options)

send this order is to frontened
