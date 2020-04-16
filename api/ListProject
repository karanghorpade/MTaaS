
package main

import (
	"fmt"
	"github.com/aws/aws-sdk-go/aws"
	"github.com/aws/aws-sdk-go/aws/awserr"
	"github.com/aws/aws-sdk-go/aws/credentials/stscreds"
	"github.com/aws/aws-sdk-go/aws/session"
	"github.com/aws/aws-sdk-go/service/devicefarm"
	//"github.com/aws/aws-sdk-go/aws/awsutil"
	//"github.com/aws/aws-sdk-go/service/devicefarm"
)

func main() {


	sess, err := session.NewSession(&aws.Config{
		Region: aws.String("us-east-2"),
	})
	creds := stscreds.NewCredentials(sess, "arn:aws:iam::345477502823:role/aws-service-role/support.amazonaws.com/AWSServiceRoleForSupport")


	svc := devicefarm.New(sess, &aws.Config{Credentials: creds})
	input := &devicefarm.ListTestsInput{
		Arn:       aws.String("arn:aws:devicefarm:us-east-2:345477502823:project:sample1"),
		NextToken: aws.String("RW5DdDJkMWYwZjM2MzM2VHVpOHJIUXlDUXlhc2QzRGViYnc9SEXAMPLE"),
	}
	
	result, err := svc.ListTests(input)
	if err != nil {
		if aerr, ok := err.(awserr.Error); ok {
			switch aerr.Code() {
			case devicefarm.ErrCodeArgumentException:
				fmt.Println(devicefarm.ErrCodeArgumentException, aerr.Error())
			case devicefarm.ErrCodeNotFoundException:
				fmt.Println(devicefarm.ErrCodeNotFoundException, aerr.Error())
			case devicefarm.ErrCodeLimitExceededException:
				fmt.Println(devicefarm.ErrCodeLimitExceededException, aerr.Error())
			case devicefarm.ErrCodeServiceAccountException:
				fmt.Println(devicefarm.ErrCodeServiceAccountException, aerr.Error())
			default:
				fmt.Println(aerr.Error())
			}
		} else {
			// Print the error, cast err to awserr.Error to get the Code and
			// Message from an error.
			fmt.Println(err.Error())
		}
		return
	}

	fmt.Println(result)
}
