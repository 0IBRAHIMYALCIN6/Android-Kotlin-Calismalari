
import androidx.appcompat.app.AppCompatActivity 
import android.os.Bundle
import android.widget.Toast
import org.csystem.android.app.calculatemachine.ProcessTools.Tools


import org.csystem.android.app.calculatemachine.databinding.ActivityMainBinding



class CalculatorActivity : AppCompatActivity() {
    private lateinit var mBinding: ActivityMainBinding
    
    private var sign = ""
    
    private var firstNumber  = StringBuilder()
    
    private var tempNumber = StringBuilder()


    private fun islemClickCallBack(situation : Tools) {

        var temp = tempNumber.toString().toDouble()
        firstNumber.append(temp)
        sign = situation.Sign
        tempNumber.delete(0, tempNumber.length)

    }
    private fun ButtonNumberCallBack(Button : Int)
    {
        tempNumber.append(Button)
        mBinding.calculatoreditNumber.setText("$tempNumber")
    }

    private fun dotCallBackButton()
    {
        if(!tempNumber.contains("."))
            tempNumber.append('.')
    }

    private fun initProcessButton()
    {
        mBinding.calculatorActivityEqualButton.setOnClickListener { equalClickCallBack() }
        mBinding.calculatorActivityClearButton.setOnClickListener { clearCallBackButton()}
        mBinding.calculatorActivityDotButton.setOnClickListener   { dotCallBackButton()  }
    }

    private fun initSignButton()
    {
        mBinding.calculatorActivityCarpma.setOnClickListener    { islemClickCallBack(Tools.CARPMA) }
        mBinding.calculatorActivityBolme.setOnClickListener     { islemClickCallBack(Tools.BOLME)  }
        mBinding.calculatorActivityCikarma.setOnClickListener   { islemClickCallBack(Tools.CIKARMA)}
        mBinding.calculatorActivityToplama.setOnClickListener   { islemClickCallBack(Tools.TOPLAMA)}
        mBinding.calculatorActivityModButton.setOnClickListener { islemClickCallBack(Tools.MOD)    }
    }

    private fun initNumberButton()
    {
        mBinding.calculatorActivityNumberButton0.setOnClickListener { ButtonNumberCallBack(NumberButton0)}
        mBinding.calculatorActivityNumberButton1.setOnClickListener { ButtonNumberCallBack(NumberButton1)}
        mBinding.calculatorActivityNumberButton2.setOnClickListener { ButtonNumberCallBack(NumberButton2)}
        mBinding.calculatorActivityNumberButton3.setOnClickListener { ButtonNumberCallBack(NumberButton3)}
        mBinding.calculatorActivityNumberButton4.setOnClickListener { ButtonNumberCallBack(NumberButton4)}
        mBinding.calculatorActivityNumberButton5.setOnClickListener { ButtonNumberCallBack(NumberButton5)}
        mBinding.calculatorActivityNumberButton6.setOnClickListener { ButtonNumberCallBack(NumberButton6)}
        mBinding.calculatorActivityNumberButton7.setOnClickListener { ButtonNumberCallBack(NumberButton7)}
        mBinding.calculatorActivityNumberButton8.setOnClickListener { ButtonNumberCallBack(NumberButton8)}
        mBinding.calculatorActivityNumberButton9.setOnClickListener { ButtonNumberCallBack(NumberButton9)}
    }

    private fun clearCallBackButton()
    {
        tempNumber.delete(0, tempNumber.length)
        mBinding.calculatoreditNumber.setText(" ")
    }

    private fun equalsLastProcess(total : Double)
    {
        mBinding.calculatoreditNumber.setText("$total")
        firstNumber.delete(0, firstNumber.length)
        tempNumber.delete(0, tempNumber.length)
        sign = ""
        tempNumber.append(mBinding.calculatoreditNumber.text.toString().toDouble())
    }

    private fun equalClickCallBack()
    {
        val number1 = firstNumber.toString().toDouble()
        val number2 = tempNumber.toString().toDouble()
        var total = 0.0

        when(sign)
        {
            "*"  -> total = number1 * number2
            "/"  -> total = number1 / number2
            "+"  -> total = number1 + number2
            "-"  -> total = number1 - number2
            "%"  -> total = number1 % number2
        }
        /*
        if(sign == "*"){
            total = number1 * number2
        }else if(sign == "/"){
            total = number1 / number2
        }else if(sign == "+"){
            total = number1 + number2
        }else if(sign == "-"){
            total = number1 - number2
        }else if(sign == "%"){
            total = number1 % number2
        }*/
        equalsLastProcess(total)
    }

    private fun initViews()
    {
        initialize()
        initNumberButton()
        initSignButton()
        initProcessButton()
    }

    private fun initialize()
    {
        mBinding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(mBinding.root)
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        initViews()
    }
}
