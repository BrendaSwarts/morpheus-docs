.. _MinimumIAMPolicies:

Minimum AWS IAM Policies
^^^^^^^^^^^^^^^^^^^^^^^^

Below are the AWS IAM Permissions covering the minimum access for |morpheus| applying to all resources and services.

See http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html for more information.


Morpheus Sample AWS IAM Policy
'''''''''''''''''''''''''''''''

.. code-block:: bash

   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "VisualEditor0",
               "Effect": "Allow",
               "Action": [
                   "autoscaling:DescribeAutoScalingGroups",
                   "ce:*",
                   "cloudwatch:GetMetricStatistics",
                   "ec2:AllocateAddress",
                   "ec2:AssignPrivateIpAddresses",
                   "ec2:AssociateAddress",
                   "ec2:AttachVolume",
                   "ec2:AuthorizeSecurityGroupEgress",
                   "ec2:AuthorizeSecurityGroupIngress",
                   "ec2:CancelExportTask",
                   "ec2:CancelImportTask",
                   "ec2:CopyImage",
                   "ec2:CopySnapshot",
                   "ec2:CreateImage",
                   "ec2:CreateInstanceExportTask",
                   "ec2:CreateKeyPair",
                   "ec2:CreateNetworkAcl",
                   "ec2:CreateNetworkAclEntry",
                   "ec2:CreateNetworkInterface",
                   "ec2:CreateSecurityGroup",
                   "ec2:CreateSnapshot",
                   "ec2:CreateTags",
                   "ec2:CreateVolume",
                   "ec2:DeleteKeyPair",
                   "ec2:DeleteNetworkAcl",
                   "ec2:DeleteNetworkAclEntry",
                   "ec2:DeleteNetworkInterface",
                   "ec2:DeleteSecurityGroup",
                   "ec2:DeleteSnapshot",
                   "ec2:DeleteTags",
                   "ec2:DeleteVolume",
                   "ec2:DeregisterImage",
                   "ec2:DescribeAccountAttributes",
                   "ec2:DescribeAddresses",
                   "ec2:DescribeAvailabilityZones",
                   "ec2:DescribeClassicLinkInstances",
                   "ec2:DescribeConversionTasks",
                   "ec2:DescribeExportTasks",
                   "ec2:DescribeImageAttribute",
                   "ec2:DescribeImages",
                   "ec2:DescribeImportImageTasks",
                   "ec2:DescribeImportSnapshotTasks",
                   "ec2:DescribeInstances",
                   "ec2:DescribeInstanceStatus",
                   "ec2:DescribeKeyPairs",
                   "ec2:DescribeNetworkAcls",
                   "ec2:DescribeNetworkInterfaceAttribute",
                   "ec2:DescribeNetworkInterfaces",
                   "ec2:DescribeRegions",
                   "ec2:DescribeSecurityGroupReferences",
                   "ec2:DescribeSecurityGroups",
                   "ec2:DescribeSnapshotAttribute",
                   "ec2:DescribeSnapshots",
                   "ec2:DescribeStaleSecurityGroups",
                   "ec2:DescribeSubnets",
                   "ec2:DescribeTags",
                   "ec2:DescribeVolumeAttribute",
                   "ec2:DescribeVolumes",
                   "ec2:DescribeVolumeStatus",
                   "ec2:DescribeVpcAttribute",
                   "ec2:DescribeVpcClassicLink",
                   "ec2:DescribeVpcClassicLinkDnsSupport",
                   "ec2:DescribeVpcEndpoints",
                   "ec2:DescribeVpcEndpointServices",
                   "ec2:DescribeVpcs",
                   "ec2:DetachNetworkInterface",
                   "ec2:DetachVolume",
                   "ec2:DisassociateAddress",
                   "ec2:ImportImage",
                   "ec2:ImportInstance",
                   "ec2:ImportKeyPair",
                   "ec2:ImportSnapshot",
                   "ec2:ImportVolume",
                   "ec2:ModifyImageAttribute",
                   "ec2:ModifyInstanceAttribute",
                   "ec2:ModifyNetworkInterfaceAttribute",
                   "ec2:ModifySnapshotAttribute",
                   "ec2:ModifyVolumeAttribute",
                   "ec2:RebootInstances",
                   "ec2:RegisterImage",
                   "ec2:ReleaseAddress",
                   "ec2:ReplaceNetworkAclAssociation",
                   "ec2:ReplaceNetworkAclEntry",
                   "ec2:ResetImageAttribute",
                   "ec2:ResetInstanceAttribute",
                   "ec2:ResetNetworkInterfaceAttribute",
                   "ec2:ResetSnapshotAttribute",
                   "ec2:RevokeSecurityGroupEgress",
                   "ec2:RevokeSecurityGroupIngress",
                   "ec2:RunInstances",
                   "ec2:StartInstances",
                   "ec2:StopInstances",
                   "ec2:TerminateInstances",
                   "ec2:UnassignPrivateIpAddresses",
                   "eks:*",
                   "iam:ListGroups",
                   "iam:ListInstanceProfiles",
                   "iam:ListRoles",
                   "rds:AddRoleToDBCluster",
                   "rds:AddTagsToResource",
                   "rds:ApplyPendingMaintenanceAction",
                   "rds:AuthorizeDBSecurityGroupIngress",
                   "rds:CopyDBClusterSnapshot",
                   "rds:CopyDBParameterGroup",
                   "rds:CopyDBSnapshot",
                   "rds:CreateDBCluster",
                   "rds:CreateDBClusterSnapshot",
                   "rds:CreateDBInstance",
                   "rds:CreateDBInstanceReadReplica",
                   "rds:CreateDBSecurityGroup",
                   "rds:CreateDBSnapshot",
                   "rds:DeleteDBCluster",
                   "rds:DeleteDBInstance",
                   "rds:DeleteDBSecurityGroup",
                   "rds:DeleteDBSnapshot",
                   "rds:DescribeAccountAttributes",
                   "rds:DescribeCertificates",
                   "rds:DescribeDBClusterParameterGroups",
                   "rds:DescribeDBClusterParameters",
                   "rds:DescribeDBClusters",
                   "rds:DescribeDBClusterSnapshotAttributes",
                   "rds:DescribeDBClusterSnapshots",
                   "rds:DescribeDBEngineVersions",
                   "rds:DescribeDBInstances",
                   "rds:DescribeDBLogFiles",
                   "rds:DescribeDBParameterGroups",
                   "rds:DescribeDBParameters",
                   "rds:DescribeDBSecurityGroups",
                   "rds:DescribeDBSnapshotAttributes",
                   "rds:DescribeDBSnapshots",
                   "rds:DescribeDBSubnetGroups",
                   "rds:DescribeEngineDefaultClusterParameters",
                   "rds:DescribeEngineDefaultParameters",
                   "rds:DescribeEventCategories",
                   "rds:DescribeEvents",
                   "rds:DescribeOptionGroupOptions",
                   "rds:DescribeOptionGroups",
                   "rds:DescribeOrderableDBInstanceOptions",
                   "rds:ListTagsForResource",
                   "rds:ModifyDBCluster",
                   "rds:ModifyDBClusterParameterGroup",
                   "rds:ModifyDBClusterSnapshotAttribute",
                   "rds:ModifyDBInstance",
                   "rds:ModifyDBParameterGroup",
                   "rds:ModifyDBSnapshotAttribute",
                   "rds:PromoteReadReplica",
                   "rds:RebootDBInstance",
                   "rds:RemoveTagsFromResource",
                   "rds:RestoreDBClusterFromSnapshot",
                   "rds:RestoreDBClusterToPointInTime",
                   "rds:RestoreDBInstanceFromDBSnapshot",
                   "rds:RestoreDBInstanceToPointInTime"
                   "rds:RevokeDBSecurityGroupIngress",
                   "route53:GetHostedZone",
                   "route53:ListHostedZones",
                   "route53:ListResourceRecordSets",
                   "s3:AbortMultipartUpload",
                   "s3:CreateBucket",
                   "s3:DeleteBucket",
                   "s3:DeleteObject",
                   "s3:DeleteObjectVersion",
                   "s3:GetBucketLocation",
                   "s3:GetObject",
                   "s3:GetObjectVersion",
                   "s3:ListBucket",
                   "s3:ListBucketMultipartUploads",
                   "s3:ListBucketVersions",
                   "s3:ListMultipartUploadParts",
                   "s3:PutObject",
               ],
               "Resource": "*"
           }
       ]
   }

Resource Filter
'''''''''''''''

If you need to limit actions based on filters you have to pull out the action and put it in a resource based policy since not all the actions support resource filters.

See http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-supported-iam-actions-resources.html for more info on limiting resources by filter.

Resource filter example:

.. code-block:: json

 {
   "Effect": "Allow",
   "Action": [
    "ec2:StopInstances",
    "ec2:StartInstances"
   ],
   "Resource": *
  },
  {
   "Effect": "Allow",
   "Action": "ec2:TerminateInstances",
   "Resource": "arn:aws:ec2:us-east-1:123456789012:instance/*",
   "Condition": {
     "StringEquals": {
        "ec2:ResourceTag/purpose": "test"
      }
    }
  }
