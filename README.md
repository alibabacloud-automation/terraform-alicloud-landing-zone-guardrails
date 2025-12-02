# terraform-alicloud-landing-zone-guardrails

Terraform module which used to setup guardrails in your landing zone environment.
Currently, this module only contains detective guardrails.

## Usage

<div style="display: block;margin-bottom: 40px;"><div class="oics-button" style="float: right;position: absolute;margin-bottom: 10px;">
  <a href="https://api.aliyun.com/terraform?source=Module&activeTab=document&sourcePath=alibabacloud-automation%3A%3Alandingzone-guardrails&spm=docs.m.alibabacloud-automation.landingzone-guardrails&intl_lang=EN_US" target="_blank">
    <img alt="Open in AliCloud" src="https://img.alicdn.com/imgextra/i1/O1CN01hjjqXv1uYUlY56FyX_!!6000000006049-55-tps-254-36.svg" style="max-height: 44px; max-width: 100%;">
  </a>
</div></div>

```hcl
module "guardrails" {
  source = "alibabacloud-automation/landingzone-guardrails/alicloud"

  detective_guardrails = [
    {
      rule_name = "sg-risky-ports-check"
      rule_identifier = "sg-risky-ports-check"
      parameters = [
        {
          name = "ports"
          value = "22,3389"
        }
      ]
      tag_scope_key = ""
      tag_scope_value = ""
    }
  ]
  config_aggreator_name = "Enterprise"
  config_aggreator_description = "All member accounts in resource directory"
  config_compliance_pack_name = "Guardrails"
  config_compliance_pack_description = "Detective guardrails"
  config_compliance_pack_risk_level = 2
}
```

* `detective_guardrails` list of config rules.
  * `parameters`, `tag_scope_key` and `tag_scope_value` is optional, depends on the rule configurations.
