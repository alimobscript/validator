# Validator

------------

Validator 由arale/validator改写，配合[alimobstyle/form](https://github.com/alimobstyle/form)实现手机端表单验证，具体用法参考[arale/validator](https://github.com/aralejs/validator)使用方法。

````html
<form action="" id="form">
    <div class="ali-field">
        <div class="ali-field-input">
            <input id="input" type="text" placeholder="电话" value="" />
        </div>
    </div>

    <div class="ali-field">
        <div class="ali-select">
            <select id="select">
                <option value="">提交类型</option>
                <option value="1">下拉列表1</option>
                <option value="2">下拉列表2</option>
            </select>
        </div>
    </div>

    <div class="ali-field">
        <label class="ali-checkbox ali-checkbox-simple">
            <input type="checkbox" id="checkbox"><span class="ali-icon icon-check"></span>同意《iHave使用协议》
        </label>
    </div>

    <div class="ali-field">
        <input type="submit" class="ali-button ali-button-orange" id="submit" value="提交" />
    </div>
</form>

<script type="text/javascript">
    window.addEventListener('load', function () {
        var interval = 500, begin = Date.now(), img = new Image(), timer = setTimeout(handler, interval);
        window.removeEventListener('load', arguments.callee);
        img.addEventListener('load', handler, false);
        img.src = 'https://i.alipayobjects.com/e/201305/Q9jNoeIir.gif?t=' + begin;

        function handler() {
            clearTimeout(timer);
            img.removeEventListener('load', handler);
            //响应在500ms以内算高速网络 高清（HD）标清（SD）
            document.body.className = (document.body.className + (Date.now() - begin < interval ? ' ali-hd' : ' ali-sd')).trim();
        }
    }, false);

    seajs.config({
        alias: {
            '$' :        'handy/jquto/1.0.2/jquto',
            'widget':    'arale/widget/1.1.1/widget',
            'validator': 'aliscript/validator/1.0.0/validator'
        }
    });
    seajs.use(['$', 'validator'], function($, Validator){
        var validator;

        validator = new Validator({
            element: '#form'
        });
        Validator.addRule('telRule', function(options){
            var _approvalReason = $.trim(options.element[0].value);

            if(_approvalReason.length < 5 || _approvalReason.length > 100){
                Validator.setMessage('telRule', '长度不符合规则');
                return false;
            }
            return true;
        }, '请输入电话号码');
        validator.addItem({
            element: '#input',
            required: true,
            rule: 'telRule',
            errormessageRequired: '请输入电话号码'
        });
        validator.addItem({
            element: '#checkbox',
            required: true,
            errormessageRequired: '请同意我们的协议'
        });
        validator.addItem({
            element: '#select',
            required: true,
            errormessageRequired: '请选择提交类型'
        });
    });
</script>
````
