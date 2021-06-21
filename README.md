account_id=`aws sts get-caller-identity --query Account --output text`

aws s3api create-bucket \
  --region us-west-2 \
  --bucket "proton-poc-templates-${account_id}" \
  --create-bucket-configuration LocationConstraint=us-west-2

tar c environment | gzip | aws s3 cp - "s3://proton-poc-templates-507414857159/environment.tar.gz" 
tar c service  | gzip | aws s3 cp - "s3://proton-poc-templates-507414857159/service.tar.gz"