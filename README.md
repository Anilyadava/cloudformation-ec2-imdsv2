# cloudformation-ec2-imdsv2
# How to spin up ec2 imdsv2
# Once the stack is deployed through cloudformation,open up the CLI and execute the following commands to enable IMDSv2

aws ec2 modify-instance-metadata-options \
        --instance-id ${instanceID} \
        --http-tokens required \
        --http-endpoint enabled
        
# Use the below commands to check the metadata of the IMDSv2 metadata

TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"`

curl -H "X-aws-ec2-metadata-token: $TOKEN" -v http://169.254.169.254/latest/meta-data/
